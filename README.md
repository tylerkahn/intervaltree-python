✨ For a **production-ready implementation** please see **@chaimleib**'s repo: https://github.com/chaimleib/intervaltree


Interval Tree in Python
=================


This is an implementation of an Interval Tree as described on [Wikipedia](http://en.wikipedia.org/wiki/Interval_tree).

Usage
---------

Objects that can be loaded into the tree must implement:

-     `get_begin()`
-     `get_end()`

which return floats or ints.



Objects are loaded into the tree during initialization:

        IntervalTree([Interval(1, 2), Interval(4, 7), Interval(1, 8)])

You can search the tree with:

-     `search(point)`
-     `search(begin, end)`

where `point`, `begin`, and `end` are of type float or int.


Example
---------


     from IntervalTree import IntervalTree

     class ScheduleItem:
         def __init__(self, course_number, start_time, end_time):
             self.course_number = course_number
             self.start_time = start_time
             self.end_time = end_time
         def get_begin(self):
             return minutes_from_midnight(self.start_time)
         def get_end(self):
             return minutes_from_midnight(self.end_time)
         def __repr__(self):
             return ''.join(["{ScheduleItem: ", str((self.course_number, self.start_time, self.end_time)), "}"])

     T = IntervalTree([ScheduleItem(28374, "9:00AM", "10:00AM"), \
                       ScheduleItem(43564, "8:00AM", "12:00PM"), \
                       ScheduleItem(53453, "1:00PM", "2:00PM")])
     T.search(minutes_from_midnight("11:00AM"), minutes_from_midnight("1:30PM"))

Which returns:

    [{ScheduleItem: (43564, "8:00AM", "12:00PM")}, {ScheduleItem: (53453, "1:00PM", "2:00PM")}]


Why?
--------

-    I need this data structure for a program I'm writing and couldn't find a good implementation that I could understand or easily extend
-    This was a good exercise. I wanted to see if I could implement a data structure from a technical specification.
-    Just started learning python - wanted to do something computer science-y


Other Stuff
-----------
-     If you see anything wrong with the implementation, please comment. I have tested it on some large datasets and it seems to work as expected.
-     Currently this implementation lacks any sort of ability to add items after instantiation. Therefore this data structure is immutable. This could either be a feature or a bug depending on your perspective :) To add other intervals to an instantiated tree `k`, you could do something like `k = IntervalTree(k.search(S, L) + [Interval(8, 12), Interval(2, 3)])` where S and L are numerical values representing the the range of values in `k`.


Hope it's useful for someone (or that you learned something)!
