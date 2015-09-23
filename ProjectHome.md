# ECTOR #
ECTOR is a learning chatterbot. pyECTOR is its python version.

ECTOR learns from what people say.
It is based on an artificial intelligence architecture, that is inspired from Copycat, an AI system from Mitchell and Hofstadter.

The Concept Network it uses is a mix between neural and semantic networks. It uses co-occurrences to compute the influence of one semantic node on another. The links are statistically weighted.

So, ECTOR does not know anything at its "birth". It's to you to teach it.

**Notice**: this is the beginning of the porting from [cECTOR](http://ector.sourceforge.net). The ConceptNetwork is working, and the answering now creates original answers.

For current development version, see [svn checkout](http://code.google.com/p/pyector/source/checkout): we should now create expression nodes.

## History ##
  * **2008-12-11** : release 0.4 - Sentence generation working
  * **2008-11-13** : release 0.3 - Basic reply (sentence-level) working
  * **2008-11-11** : release 0.2 - Basic entry parsing working
  * **2008-11-05** : release 0.1 - Functional ConceptNetworkModule!

&lt;wiki:gadget url="http://www.ohloh.net/p/25724/widgets/project\_basic\_stats.xml" height="220"  border="1" /&gt;