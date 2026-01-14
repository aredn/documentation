==========================
The Babel Routing Protocol
==========================

*Contributor: Tim Wilkerson KN6PLV*

The AREDN® team implemented a new routing protocol called `Babel <https://www.irif.fr/~jch/software/babel/>`_ which replaced the original and obsolete protocol called OLSR. Babel has a number of qualities which make it good for AREDN®.

1. It’s a loop free protocol so, regardless of how the network is changing, routing loops will never form in the network.
2. It’s primarily a reactive protocol which sends changes to neighbors when needed rather than broadcasting its state continually.
3. The protocol understands the difference between wired, wireless, and tunneled links – the three link types AREDN® utilizes.
4. It’s a layer-3 routing protocol, which integrates easily with how AREDN® already operates.
5. It’s highly configurable which will allow an optimal setup for our use case.
6. Finally, it’s simple.

If you’re interested in more comparisons between Babel and other options, there are many good presentations on YouTube. `This <https://www.youtube.com/watch?v=1zMDLVln3XM>`_ is a great primer on Babel itself.

Babel was initially deployed alongside OLSR with the two operating in parallel. This allowed us to examine Babel's performance in our networks without disturbing nodes which were not running Babel. The results indicated that Babel outperformed OLSR in several areas, providing a more stable network, better routing decisions, and lower network overhead.
