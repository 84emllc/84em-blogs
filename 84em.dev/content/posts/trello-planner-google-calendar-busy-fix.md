---
title: "Trello Planner Doesn't Mark You as Busy in Google Calendar. Here's How to Fix It."
date: 2026-02-10
slug: "trello-planner-google-calendar-busy-fix"
description: "Trello Planner creates Focus Time events that don't mark you as busy in Google Calendar. A free Google Apps Script fixes it in five minutes."
tags: ["trello", "google-calendar", "productivity", "automation", "tools"]
---

Trello's Planner feature lets you drag cards onto a calendar to block time for tasks. It syncs with Google Calendar, which sounds useful. The problem is how it syncs.

Every card you drag onto the Planner creates a Focus Time event in Google Calendar. Focus Time events don't automatically decline conflicting meetings unless you manually enable that on each event. Trello doesn't give you a way to change this.

If you're using Planner to block time for client work, your calendar still looks open to anyone trying to book a meeting with you. That defeats the purpose.

## The Fix

Google Apps Script can watch your calendar and fix those Focus Time events automatically. It can either enable the auto-decline flag so meetings get rejected, or convert them into regular busy events. It's free, runs in the background, and takes about five minutes to set up.

The script scans your calendar every 15 minutes. When it finds a Focus Time event created by Trello, it enables the auto-decline flag and sets the status to Do Not Disturb. Meetings that conflict with your focus time get declined automatically.

## Setup

### Create the Script

Go to [script.google.com ↗](https://script.google.com) and click New project. Delete any existing code in the editor. Paste in the [full script below](#the-script) and save it.

### Enable the Google Calendar API

In the left sidebar, find Services and click the + icon next to it. Scroll to Google Calendar API (not "Google Calendar" — the one that specifically says "API") and click Add. You should see "Calendar" appear under Services in the sidebar.

### Authorize the Script

In the function dropdown at the top of the editor, select fixFocusTimeEvents and click Run. A dialog will ask you to review permissions. Click through it, select your Google account, and click Allow.

If you see "Google hasn't verified this app," click Advanced, then "Go to [project name] (unsafe)." This is normal for personal scripts.

### Schedule the Script

In the function dropdown, select createTrigger and click Run. This sets the script to run automatically every 15 minutes. You only need to do this once.

### Verify It's Running

Click the Triggers icon (clock) in the left sidebar. You should see an entry for fixFocusTimeEvents set to every 15 minutes. To see a log of past runs, click Executions in the sidebar.

To test it immediately, drag a card onto Trello Planner, then manually run fixFocusTimeEvents from the editor. The Focus Time event should now have auto-decline enabled.

## Configuration

The script has two modes. The default mode keeps Focus Time events but enables auto-decline so conflicting meetings get rejected. It also sets chat status to Do Not Disturb. The alternative mode deletes the Focus Time event and recreates it as a regular busy event.

The script scans 30 days ahead by default. All three settings are controlled by variables at the top of the script. Change them to match what you need.

## The Script

```javascript
/**
 * Trello Planner Focus Time Fixer
 *
 * Finds focus time events created by Trello and ensures they
 * show as "busy" and optionally auto-decline conflicting meetings.
 *
 * Setup:
 * 1. Go to https://script.google.com and create a new project
 * 2. Paste this code in
 * 3. Enable the Google Calendar API advanced service:
 *    - Click "Services" (+ icon) in the left sidebar
 *    - Find "Google Calendar API" and click Add
 * 4. Run fixFocusTimeEvents() manually first to authorize
 * 5. Run createTrigger() once to set up automatic runs every 15 minutes
 */
// How far ahead to scan for events (in days)
var LOOK_AHEAD_DAYS = 30;
// Set to true if you want focus time events to auto-decline meetings
var ENABLE_AUTO_DECLINE = true;
// Set to true to convert focus time events into regular busy events instead
var CONVERT_TO_REGULAR_EVENT = false;

function fixFocusTimeEvents() {
  var now = new Date();
  var future = new Date();
  future.setDate(future.getDate() + LOOK_AHEAD_DAYS);

  var events = Calendar.Events.list('primary', {
    timeMin: now.toISOString(),
    timeMax: future.toISOString(),
    eventTypes: ['focusTime'],
    singleEvents: true,
    maxResults: 100
  });

  if (!events.items || events.items.length === 0) {
    Logger.log('No focus time events found.');
    return;
  }

  var fixed = 0;

  for (var i = 0; i < events.items.length; i++) {
    var event = events.items[i];
    var needsUpdate = false;
    var patch = {};

    if (CONVERT_TO_REGULAR_EVENT) {
      // Delete the focus time event and recreate as a regular busy event
      var newEvent = {
        summary: event.summary || 'Trello Task',
        start: event.start,
        end: event.end,
        description: event.description || '',
        transparency: 'opaque' // busy
      };

      Calendar.Events.remove('primary', event.id);
      Calendar.Events.insert(newEvent, 'primary');
      fixed++;
      Logger.log('Converted to regular event: ' + (event.summary || event.id));
      continue;
    }

    // Alternative: keep as focus time but ensure busy + auto-decline
    if (event.transparency === 'transparent') {
      patch.transparency = 'opaque';
      needsUpdate = true;
    }

    if (ENABLE_AUTO_DECLINE) {
      if (!event.focusTimeProperties ||
        event.focusTimeProperties.autoDeclineMode !== 'declineAllConflictingInvitations') {
        patch.focusTimeProperties = {
          autoDeclineMode: 'declineAllConflictingInvitations',
          declineMessage: 'Declined — busy with scheduled work.',
          chatStatus: 'doNotDisturb'
        };
        needsUpdate = true;
      }
    }

    if (needsUpdate) {
      Calendar.Events.patch(patch, 'primary', event.id);
      fixed++;
      Logger.log('Updated: ' + (event.summary || event.id));
    }
  }

  Logger.log('Fixed ' + fixed + ' events.');
}

/**
 * Run this once to create a trigger that checks every 15 minutes.
 */
function createTrigger() {
  // Remove existing triggers first
  var triggers = ScriptApp.getProjectTriggers();
  for (var i = 0; i < triggers.length; i++) {
    if (triggers[i].getHandlerFunction() === 'fixFocusTimeEvents') {
      ScriptApp.deleteTrigger(triggers[i]);
    }
  }

  ScriptApp.newTrigger('fixFocusTimeEvents')
    .timeBased()
    .everyMinutes(15)
    .create();

  Logger.log('Trigger created. fixFocusTimeEvents will run every 15 minutes.');
}

/**
 * Run this to remove the automatic trigger.
 */
function removeTrigger() {
  var triggers = ScriptApp.getProjectTriggers();
  for (var i = 0; i < triggers.length; i++) {
    if (triggers[i].getHandlerFunction() === 'fixFocusTimeEvents') {
      ScriptApp.deleteTrigger(triggers[i]);
    }
  }
  Logger.log('Trigger removed.');
}
```

## Why This Matters

Tools should work the way you expect them to. If you block time on your calendar, that time should be blocked. Trello's Planner gets this wrong, but a free script running in the background can fix it.
