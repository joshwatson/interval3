# interval3
interval3 is a fork of the original interval module by Jacob Page. This version is compatible with python 2.7 and python 3.

The interval3 module provides the `Interval` and `IntervalSet` data types. `Interval`s describe continuous ranges that can be open, closed, half-open, or infinite. `IntervalSet`s contain zero to many disjoint sets of `Interval`s.

## Installation

`pip install interval3`

## Examples
Intervals don't have to pertain to numbers.  They can contain any data 
that is comparable via the Python operators `<`, `<=`, `==`, `>=`, and `>`. Here's 
an example of how strings can be used with Intervals:
```python
>>> volume1 = Interval.between("A", "Foe")
>>> volume2 = Interval.between("Fog", "McAfee")
>>> volume3 = Interval.between("McDonalds", "Space")
>>> volume4 = Interval.between("Spade", "Zygote")
>>> encyclopedia = IntervalSet([volume1, volume2, volume3, volume4])
>>> mySet = IntervalSet([volume1, volume3, volume4])
>>> "Meteor" in encyclopedia
True
>>> "Goose" in encyclopedia
True
>>> "Goose" in mySet
False
>>> volume2 in (encyclopedia ^ mySet)
True
```

Here's an example of how times can be used with Intervals:
```python
>>> officeHours = IntervalSet.between("08:00", "17:00")
>>> myLunch = IntervalSet.between("11:30", "12:30")
>>> myHours = IntervalSet.between("08:30", "19:30") - myLunch
>>> myHours.issubset(officeHours)
False
>>> "12:00" in myHours
False
>>> "15:30" in myHours
True
>>> inOffice = officeHours & myHours
>>> print inOffice
['08:30'..'11:30'),('12:30'..'17:00']
>>> overtime = myHours - officeHours
>>> print overtime
('17:00'..'19:30']
````
