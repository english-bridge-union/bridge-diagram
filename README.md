# bridge-diagram

A simple javascript snippet to quickly generate bridge deal/bidding diagrams.

## Example

```
<div id="diagram">
  
{dnnone 
  Q106 KQ973 4 A642;
  J4 J654 K7653 J10;
  A8532 A8 AJ10 Q93;
  K97 102 Q982 K875 
}

{b.1hp1sp2cp2dp2sp4s/}
  
4!s is a normal enough contract, and so the key is how many tricks will be made.
West will probably lead a diamond, which gives declarer the opportunity to take 
a ruffing finesse in the suit on the second round. Now it is a matter of making 
a good guess in trumps. If West plays low when a trump is led from the South 
hand, declarer will make only ten tricks if the ten is played, but there is an 
opportunity to end up with twelve tricks on the correct guess. If West rises 
with the king, declarer will make eleven. So, I expect the field to be divided 
between these three results, with the odd pair in 3NT, and some getting too 
high.

</div>
```
The above HTML gets converted, with a single line of javascript, to this:

![](https://github.com/english-bridge-union/bridge-diagram/raw/master/diagram.PNG "Bridge Article")

## What's the point?

Formatting bridge diagrams and auctions for the web can be quite fiddly, so this is a quick and simple way to write bridge content and have it look uniform and attractive. Once the syntax is learned, you can knock out a bridge diagram in seconds without having to remember how to class your `div`s.

It's fairly easy to extend if you want to customise this for your own purposes. You'll want to know Javascript to deal with the parser, CSS to deal with the formatting and SVG to deal with the vulnerability/dealer graphic.

## Installation

You only need parser.js and diagram.css from this repository. Add them to your HTML header, place the text to be converted into a convenient `<div>` and then run the parser.parse function on the text. For example:

```
<script>
  var x = document.getElementById('diagram');
  x.innerHTML = parser.parse(x.innerHTML);
</script>
```

The test.html file might be a useful starting point if this isn't clear.

## Syntax

### Suit Symbols

This is the simple one. An exclamation mark followed by a c/d/h/s character will be converted into the corresponding suit symbol, of the appropriate colour.

### Hand Diagram

Hand diagrams look like this:

```
{dnnone 
  Q106 KQ973 4 A642;
  J4 J654 K7653 J10;
  A8532 A8 AJ10 Q93;
  K97 102 Q982 K875 
}
```

Some white space is ignored, so you could equally write this:

```
{dnnone Q106 KQ973 4 A642;J4 J654 K7653 J10;A8532 A8 AJ10 Q93;K97 102 Q982 K875}
```

`{d` starts off a diagram. The next character shows the dealer (`n`/`e`/`s`/`w`) and the text after that shows the vulnerability (`both`/`none`/`ns`/`ew` with `b`/`0`/`-` also being allowed). These are optional, but if you have a vulnerability without a dealer then you need to put `-` as the dealer.

After that the four hands are shown, separated by semi-colons, in the order North/East/South/West. Each hand gives the four suits, in descending order and separated by spaces. To show a void, use a `-`. A `10` can also be shown as a `T`.

Finally, a `}` finishes the hand diagram.

### Bidding Diagram

Showing an auction looks like this:

```
{b
  . 1h p 1s
  p 2c p 2d
  p 2s p 4s
  /
}
```

White space is ignored, so you could equally write this:

```
{b.1hp1sp2cp2dp2sp4s/}
```

`{b` starts off a bidding diagram, after which there are 0-3 full stops to indicate where the bidding starts. e.g. if East is dealer, you would start with `{b..` to show that West and North don't act.

After that, simply enter the auction in the order that it happens. `p` or `-` means PASS, `x` means DOUBLE and `r` means REDOUBLE. A `/` means ALL PASS. No-Trumps are `n`, not 'nt'.

Finally, a `}` terminates the bidding diagram.

## Extending it

### If you don't like the language

Perhaps you don't want to start a bidding diagram with `{d`, or you want to add support for highlighting the opening lead. You'll need to edit the parser grammar to do this. The parser was built using PEG.js, and the simplest way to generate your own is to use [the tool on their website](https://pegjs.org/online). Take the contents of the grammar.txt file and copy that into the tool. You can then edit it, test it and compile a new version from there.

### If you don't like the layout

If you want a fixed-width font, or a border around the bidding diagram, you'll need to edit the CSS file. It was generated with Sass, which is much easier to edit, so we've made that file available too.

### If you don't like the compass image

The compass image is an SVG graphic, and to change it you'll need to edit the grammar (see above). All the code for the compass is contained in the drawCompass function, so that should be all you have to edit.

## Compatibility

This uses CSS Grid, so probably won't work on Internet Explorer.
