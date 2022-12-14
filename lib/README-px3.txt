PX3 - a Backbone style framework
--------------------------------

PX3 is an MV*, Backbone-like framework with a more consistent design:

   - objects are also containers, of type Model or View

   - named getters and setters, including loud getters

   - containers can be specialized so they only contain a specific
     type of object and also contain members

   - Views derived from Model, so they can have members and
     getter/setters and be containers
   
   - objects that 'contain' other objects (by using 'set', 'add',
     'push' or 'insertAt' methods) are passed messages from the
     objects they contain, just like Backbone collections but more
     general.

   - iterators (start,end,next,prev,current), standard mapping
     functions (map, each, forIn) and sorting.

If you don't like the fact you can't have collections of collections
or that views and collections can't have settable members in Backbone,
then PX3 is for you.

Installation
------------

    npm install --save px2
    bower install --save px2

Dependencies
------------

    jQuery if you use Views, none otherwise.

Examples
--------

     See the examples/ folder.

Model methods
-------------

     this.create(name, value, silent):

       Creates a new member variable called 'name' with initial value
       of 'value'. Also creates named getters/setters, this.name() and
       this.name(value). Sends 'create' and 'create:$name' messages
       with value as event.value unless silent is true.

     this.copy():

       Returns a deep copy of this.

     this.set(name, value, silent)

       Standard setter for Model objects. Sends "change" and
       "change:$name" events when called, unless silent is true.  The
       value of this.name() is the new value and the event.value
       (passed as the first part of 'change' trigger handler) is the
       old value that this.name() was set to.

     this.get(name, loud)

       Standard getter for Model objects, sends 'get' and 'get:$name'
       messages. Will send 'get' and 'get:$name' messages if 'loud' is
       true, with the event value being the previous value of
       this.name(). This message is sent before the value is returned
       allowing the opportuntity to change the value that is going to
       be returned to the calling function.  This allows for the
       creation of named variables that return a different value
       everytime they are called:

          // Create a random variable
          obj.create('random');
          obj.on('get:random', function (e) {
              return this.random(Math.random());
          });
          var a = obj.get('random', true);
          expect(obj.get('random', true)).to.not.equal(a);
  
     this.add(value, silent)

       Add value to the collection if it is not already in the
       collection and sends "add" with event.target being the value
       added and "modified" with event.target being an array with the
       value added, unless silent is true.
       
     this.insertAt(i, value, silent)

       Add value to the collection at index i. Sends "add" with
       event.target being the value added and "modified" with
       event.target being an array with the value added, unless silent
       is true.
       
     this.push(value, silent)

       Add value to the head of the collection. Sends "add" with
       event.target being the value added and "modified" with
       event.target being an array with the value added, unless silent
       is true. Much faster than add, since it doesn't have to scan
       the entire storage looking for a duplicate.
       
     this.swap(i, j, silent)

       Exhanges two values in the collection. Sends "modified" with
       event.target being an array with the values swapped, unless
       silent is true.
       
     this.remove(value, silent)

       Remove value from the collection if it has been added to it
       using add/push/insertAt. Sends "add" with event.target being
       the value added and "modified" with event.target being an array
       with the value added, unless silent is true. Returns true if
       the object was removed, false otherwise.

     this.at(index)

       Return an element in the collection located at index.  Throws
       Error if index is out of range.
       
     this.indexOf(obj)

       Return the integer index of obj in storage (for use with at), or
       undefined if the object is not in the collection.
       
     this.length:

       The number of elements contained in the object storage.

     this.clear(silent)

       Remove all items from the collection and sets length to 0;
       sends "modified" message with all items from storage before
       clearing, unles silent is true.

     this.on(message, function (event) { ... }, self)

       Intercept message with handler, setting this to self during
       call of handler.  If 'self' is omitted, 'this' is used.
       'event' contains event.value, which is the value passed to
       trigger, and event.target which will be the object that
       triggered the message, in most cases 'this'.

       If the event handler returns true, messages will continue to
       propagate up the containment chain, else it will stop at the
       handling object.

     this.once(message, function (event) { ... }, self)

       Like this.on, but the handler is only called once, after which
       it is removed from the handler action table.

     this.trigger(message, value)

       Send the message to this, and then all containing parents,
       recursively up the containment tree.  Propagation stops when
       the message is intercepted and handled, unless the handler
       returns true (and only true, not truthy).

     this.each(function (value) { ... }, self)

       Side effects only iteration over elements. 'self' defaults to
       'this' if not provided.

     this.map(function (value) {...}, self)

       Returns an array of returned values from function. 'self'
       defaults to 'this' if not provided.

     this.forIn(function (key, value) { ... }, self)

       Side effects only mapping over members (created with
       this.create()); 'self' defaults to 'this' if not provided.

     this.find(object || function (value) ...)

       Find a specific object in the collection.  If the argument is
       an object, === is used, if a function it is called with each
       element of the collection until it returns true. Returns the
       object, if it is found.

     this.sort(fun, silent)

        Destructively sorts the internal storage array using fun,
        returns 'this' so you can chain with map. Sends "modified"
        event with the sorted array, unless silent is true.

Iterators
---------

      All iterators send "change" and "change:current" messages unless
      silent is true, with the event.value being the previous value of
      this.current().

      Note: the pattern for iterators is slightly different than other
      languages:

          for(var i = this.start(); i; i = this.next()) { ... }

      or in reverse:
      
          for(var i = this.end(); i; i = this.prev()) { ... }

      this.start(silent)

        Select the first element of storage as current.

      this.end(silent)

        Select the last element of storage as current.

      this.current(objOrNumber, silent)

        Return the current element with no aruments.  With obj as an
        argument, select that object as the current object.  With a
        number, select the object at that index in storage as current.

     this.next(loop, silent)

        Return the next element and set it as current, or undefined if
        at the end of storage.  If loop is true, loop around to the
        start and return the first element.
        
     this.prev(loop, silent)

        Return the previous element and set it as current, or
        undefined if at the start of storage.  If loop is true, loop
        around to the end and return the last element.

Events
------

      An event is passed to a trigger handler.  An event includes the
      value and target fields; value is the value passed to
      set/add/push/etc, and target is the object that initiated the
      event.

Serialization
-------------

       Serialization is working but some parts are experiemntal, so
       don't expect it to work perfectly yet with all/complex
       Models/Views.  Try it at first with simple objects that have
       only members and storage and not complex actions (trigger that
       set setf to something other than this) See test/serialize.js
       for more info on what works and what doesn't..

       this.serialize()

          Return an object containing all members, storage and actions
          that can be possibly passed to JSON.stringify() for storage.

       this.load(object, load-actions)

          Load 'object' into this.  'Object' should be something that
          was returned from this.serialize(), probably after being
          JSONified and back. If load actions is false, actions are
          not loaded into this, hopefully keeping them from getting
          trashed during the load (needs more testing and
          experimentation).


Example of defining and using a Model as an object and a container
------------------------------------------------------------------

    var Model = require("px2").Model;
    
    // Declare object class data
    var Point = Model({
        // Optional, but good for debugging and containers
        type: 'Point'

        // optional, create members and set default values 
        defaults: {
            system: "cartesian"
        },
    
        // Constructor, called during instatiation
        init: function (x, y) {
            this.create('x', x);
            this.create('y', y);
        }
    
        // A random method
        toString: function () {
            return "x: " + this.x() + ", y: " + this.y() + " " + this.system();
        }
    })
    
    // Delcare a container
    var Points = Model({
        type: 'Points',
    
        // This container contatins type...
        contains: 'Point'
    
        init: function () {
            this.create('currentPoint'); // undefined initially
    
            this.on('add', function (e) {
                // Use a named setter to set the current value of member 'currentPoint'.
                // e is passed to all trigger functions and it contains:
                //          e.value: the value that was added/removed/updated/etc
                //          e.target: the object that was updated, in this case it would be 'this'
                this.currentPoint(e.value);
            });
            this.on('remove', function (e) {
                if(e.value === this.currentPoint()) {
                    this.currenPoint(undefined);
                }
            });
        }
    });
    
    // Instantiate a Points collection
    var points = new Points();
    
    points.add(new Point(100, 200));
    
    var point = points.at(0);
    
    var xs = points.map(function (point) {
        return point.x();
    }); // => [100]
    
Views
-----

Views are derived Model and contain all features and methods that
Models give.

View example
------------

    var PointsView = View({
        // optional, but handy for debugging and is the default class if
        // className is not defined (below)
        type: 'PointsView',

        // Set the name of the variable used to reference the model,
        // in this case this.points rather than this.model
        model "points"
    
        // optional, sets default tag name of this.$el, else is "div"
        tagName: "span",  
    
        // optional, sets default class of this.$el. If not provided
        // the class name is set the the value of type (above). If the
        // string starts with a space, the provided class name(s) will be
        // appended to the value of type. ie: a value of className: " window"
        // will result in a final class name of "PointsView window"
        // in this case.
        className: " window",
    
        // optional, name for this.model. In this case, you could use
        // this.points to reference your model. The model is not
        // enclosed in the object, so messages from the model are
        // not propagated into this View.
        model: 'points',

        // optional css initial style, using jquery syntax
        style: {
               "font-weight": "bold"
        }
    
        // events, just like backbone
        events: {
            'click': function (e) {
                     alert(this.message()); // 'this' is bound for you automagically
            }
        }
    
        init: function (model, value) {
              this.create('value', value);
              this.create('message', "Hello World!");

              // eithefq this.model or this.points can be used, due to
              // the 'model' option used above
              this.points.on('add', this.render); // 'this' is bound automagically

              // this.render() is automatically called at the end of init for Views.
        }
    
        // render, which if you don't provide a default is given that
        // just returns this.$el
        render: {
                return this.$el.html(this.points.map(function (v) {
                    return $('<div>').text(v.toString());
                }));
        }
    })

    var points = new Points();

    // A View constructor is similar to a Model constructor, but the
    // first argument is *always* the model for the view.
    var pointsView = new PointsView(points, 1);
    $('document').ready(function () {
        $('body').html(pointsView.$el);
    });


What is this written in?
------------------------

PX3 was originally written in Parenscript: 
    https://github.com/vsedach/Parenscript

Now it's been compiled to Javascript, but the parenscript code is
still in the source file as comments before each line.  The original
source is at https://github.com/burtonsamograd/px2.

To build from source you need sigil: https://github.com/burtonsamograd/sigil or even easier:

   $ npm install -g sigil-cli

--
Burton Samograd
2022


