# Treeline

Treeline turns indented-line input into a tree structure.

Given a sequence of lines with varying levels of indentation, like this:

    line 1
      line 2
      line 3
        line 4
      line 5
      
Treeline will produce a hash like this:

    {
      "line 1" => {
        "line 2" => {},
        "line 3" => {
          "line 4" => {},
        },
        "line 5" => {},
      },
    }

## Installation

    $ gem install treeline

## Usage

The `parse` method on `Treeline::Parser` does the heavy lifting.

    parser = Treeline::Parser.new
    tree = parser.parse lines
    
The parser is bone-headed simple. The first line of input is taken to be the root of a new tree.
For each subsequent line, the amount of indentation is compared to the amount in the previous line, and

* if the indentation is the same, the new line is added as a sibling of the previous;
* if the indentation is greater, the new line is added as a child of the previous; or
* if the indentation is less, the parser climbs back towards the root until one of the previous
  two rules applies.

`parse` optionally takes a block. Each line of the input will be passed to the block, which should
return the line modified as desired. For instance, to force all of the text to lowercase:

    parser = Treeline::Parser.new
    tree = parser.parse(lines) do | line |
      line.downcase
    end
    
The block is called *before* the amount of indentation is determined, so you can change the indentation
if you want to.
    
## Dependencies

None at the moment.

## Support

[wiki](https://github.com/CraigCottingham/treeline/wiki "wiki")

## License

Copyright &copy; 2011 Craig S. Cottingham.
It is free software, and may be redistributed under the terms specified in the LICENSE file.