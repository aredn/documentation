==========================
The Babel Routing Protocol
==========================

*Contributor: Tim Wilkerson KN6PLV*

The AREDN® team introduced a new routing protocol with the ultimate goal of replacing OLSR. OLSR has many faults which AREDN® has lived with for a long time, so for the last couple of years we’ve been looking at alternatives and making incremental changes to the codebase to allow us to introduce something better. We have now added `Babel <https://www.irif.fr/~jch/software/babel/>`_ to AREDN®.

Babel has a number of qualities which make it good for AREDN®. First, it’s a loop free protocol so, regardless of how the network is changing, routing loops will never form in the network. Second, it’s primarily a reactive protocol which sends changes to neighbors when needed rather than broadcasting its state continually. Third, the protocol understands the difference between wired, wireless, and tunneled links – the three link types AREDN® utilizes. Fourth, it’s a layer-3 routing protocol, which integrates easily with how AREDN® already operates. Fifth, it’s highly configurable which will allow an optimal setup for our use case. Finally, it’s simple.

We considered a number of options, and another contender was *BATMAN Advanced*. Unfortunately it is not a good fit for AREDN® as it primarily focuses on level-2 wireless networking. AREDN® needs a protocol which can do more. We evaluated how we could use BATMAN and it wasn’t simple, efficient, or pretty. If you’re interested in more comparisons between Babel and other options, there are many good presentations on YouTube. `This <https://www.youtube.com/watch?v=1zMDLVln3XM>`_ is a great primer on Babel itself.

Babel was initially deployed alongside OLSR with the two will operating in parallel. If there is a Babel path between two nodes in the network, then Babel routes will be used to send traffic. If not, then OLSR routes will be used. This allows us to deploy Babel and examine its performance in our networks without disturbing nodes which are not running Babel. Be aware that older radios with limited memory – the ones using the *tiny* firmware images – will not be able to support both protocols and should be replaced rather than upgraded.

Evaluating success will depend on a few things, and the more feedback from the community the better. Our goals are to provide a more stable network, better routing decisions, and lower network overhead. Assuming success, the timeframe to replace OLSR will be measured in years. Once OLSR is gone, any node not running Babel will disconnect, and we don’t want to leave our users behind, so we are giving this as much time as possible for the transition to the newer protocol.
