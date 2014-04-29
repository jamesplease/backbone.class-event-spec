Class Event Specs
====================

The specifications for Marionette Class Events.

### About

Many Marionette Classes have important events that happen to them. An example is a region showing a view within its
element. Those familiar with Marionette know that there is a before and after event associated with this Class Event,
and also before and after callbacks. This collection of activities around the primary event is collectively called a Class Event.

These specifications provide the guidelines on how to create a new Class Event for your Classes that follow this same pattern.

The internal methods of Marionette should **always** adhere to these specifications, and it is highly recommended
that you, in your application, also follow the specs.

### Precedent

The precedent for Class Events is the Backbone Event system, and, in particular, [the built-in list
of Events](http://backbonejs.org/#Events-catalog). At all times the Class Events specifications should
be consistent with that catalogue of events. Should Backbone's event system change, then the Class Events
specification should also change to remain consistent.

Because of this precedent we will begin by studying Backbone Events in greater depth:

#### Anatomy of a Backbone Event

Events in the Backbone universe follow the following format:

`action:subject`

##### Action

The action is always present tense. The action should be a simple verb that describes the event
that just happened.

```js
// Bad Backbone event name
'rendered:view';

// Good Backbone event name
'render:view';
```

##### The Separator

The separator in events is a colon, `:`. The colon should be used instead of other
separation mechanisms, such as hyphenating and camelcase.

```js
// Events that use an incorrect separator
'show:myView';
'show:my-view';

// Events that use a correct separator
'show:my:view';
```

##### Subject

If the action is acting on a particular thing, then you may pass along the subject which is separated from the
action by a colon. Keep in mind that the subject is always optional. An event may have at most
a single subject.

The subject is ideally a simple, one-word noun. In the case of a more complex noun you should use colons
to separate out the pieces.

```js
// If you must use more complex nouns use the colon separator
'show:scrolling:view';
```

It is suggested that you avoid composite nouns if possible.

### Class Events

#### Anatomy of a TriggerMethod

Every Class Event is wrapped by two triggerMethod calls: one before the event and one afterward. TriggerMethod
triggers the event on the class' event bus while also executing a function for that event. So, for instance, 

TriggerMethod events differs slightly from Backbone events. They have the following form:

`adverb:verb:subject`

##### Adverb

The adverb is either `before` or nothing at all.

#### Synchronous/Asynchronous

Trigger Methods events are asynchronous. This means that asynchronous methods in the `onBefore` callback will
not be necessarily be executed before the event itself occurs.

#### Anatomy of a Class Event

A class event has three components.

1. A before triggerMethod event
2. The event itself
2. An after triggerMethod event

##### The Before TriggerMethod

The before event callback has the following form

`before:action:subject`

This causes the following method to be triggered:

`onBeforeActionSubject`

##### The Event Itself

The event itself is whatever action is being completed. This takes place in-between the trigger method calls.

##### The After TriggerMethod

The after event callback has the same form as a Backbone event.

`action:subject`

This causes the following method to be triggered:

`onActionSubject`
