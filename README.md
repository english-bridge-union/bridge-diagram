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

[](https://github.com/english-bridge-union/bridge-diagram/raw/diagram.PNG "Bridge Article")
