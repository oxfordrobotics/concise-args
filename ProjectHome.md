Are you frustrated with the amount of code that you need to write to parse command line arguments? Well then concise-args is for you!

It is a simple command line argument parser that allows very concise syntax.

There is only a [single header](http://code.google.com/p/concise-args/source/browse/trunk/ConciseArgs.hpp), with no dependancies other than the normal STL containers.


The goal was to require as few lines of code as possible to parse options passed in using the standard -c/--longName= syntax.


For example, to parse 4 flags requires 6 lines of code:
```
#include <ConciseArgs>
int main(int argc, char ** argv)
{
  bool bl = false;  int in;  float flt = -9; double dbl=3.14;
  ConciseArgs parser(argc, argv);
  parser.add(bl,  "b", "bools", "do bools work?"); // Parse -b/--bools, setting bl accordingly
  parser.add(in,  "i", "ints",  "do ints work?", true); // The "true" means this argument is mandatory
  parser.add(flt, "f", "floats"); //I'm too lazy to provide a description
  parser.add(dbl, "d"); //I'm too lazy to even provide a longName
  parser.parse();
  return 0;
}

```

This would set the create the following help/usage message:
```
$ ./concise-args-test -h
Usage:
  concise-args-test [opts] 
Options:
  -h, --help   = [true]       : Display this help message
  -b, --bools  = [false]      : do bools work?
  -i, --ints   = <int32_t>    : do ints work?
  -f, --floats = [-9.00000]   : 
  -d           = [3.14000]    : 

```