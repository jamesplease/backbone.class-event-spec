trigger-method-specs
====================

The specifications for Marionette triggerMethod.

### About

The TriggerMethod API is a consistent, unified means to handle events and callbacks within
your Classes. These specifications outline the best practices for working with TriggerMethods. The
internal methods of Marionette should **always** adhere to these specifications, and it is highly recommended
that you, in your application, also follow the specs.

### Precedent

The precedent for TriggerMethods is the Backbone Event system, and, in particular, [the built-in list
of Events](http://backbonejs.org/#Events-catalog). At all times the TriggerMethod specifications should
be consistent with that catalogue of events. Should Backbone's event system change, then the TriggerMethods
specification should also change to remain consistent.

### Anatomy of a Backbone Event

Events in the Backbone universe should follow the following format:

`action:subject`

#### The Separator

The separator in events is a colon, `:`. The colon should be used instead of other
separation mechanisms, such as hyphenating and camelcase.

```js
// Events that use an incorrect separator
'show:myModel';
'show:my-Model';

// Events that use a correct separator
'show:my:model';
```

#### The Action

The action is always present tense. The action should be a simple verb that is as descriptive
of what is going on as possible.

```js
// Bad Backbone event name
'rendered:model';

// Good Backbone event name
'render:model';
```

#### The Subject

If the action is acting on a particular object, then you may pass along the subject, separated from the
action by a colon. Keep in mind that the subject is always optional. An event may have at most
a single subject.

The subject is ideally a simple, one-word noun. In the case of a more complex noun you should use colons
to separate out the pieces.

```js
// If you must use more complex nouns use the colon separator
'show:big:model';
```

It is suggested that you avoid composite nouns as much as possible.

### Anatomy of a Trigger Method

A trigger method has three components.

1. A before event/callback trigger.
2. The event itself
2. An after event/callback trigger

A triggerMethod event differs slightly from a Backbone event. It has the following form:

`adverb:verb:subject`

Where the adverb is either `before` or nothing at all.

#### The Before Event/Callback

The before event callback has the following form

`before:action:subject`

This causes the following method to be triggered:

`onBeforeActionSubject`

#### The Event Itself

The event itself is whatever action is being completed. This takes place in-between the trigger method calls.

#### The After Event/Callback

The after event callback has the same form as a Backbone event.

`action:subject`

This causes the following method to be triggered:

`onActionSubject`

### Synchronous/Asynchronous

Trigger Methods events are asynchronous. This means that asynchronous methods in the `onBefore` callback will
not be necessarily be executed before the event itself occurs.