# Econet Island

This page has been created to co-ordinate the assignment of Econet Addresses for those bringing Econet gear to [Acorn World 2009](http://www.acornworld.co.uk).

# Suppliers of Hardware / Station IDs

| Station ID | Machine | Owner | Changeable | Notes |

|------------|---------------------------|----------------|------------|---------------------------------------------------------------------------------------------------|

| 1-4 | Bs/Masters | Rob O'Donnell | No | Viewdata BBS stations. (since \*who counts from 1 ..) |

| 5-8 | BeebEm | Rob O'Donnell | No | Viewdata BBS stations. (on AUN, but reserved to avoid config clashes) |

| 23 | Unknown | J.G.Harston | ?? | |

| 30 | Atom | Ian Stocks | Yes | |

| 40 | BBC Master | David Glover | Yes | With GoMMC and 6502 co-pro (Which is sometimes broken) |

| 50 | BBC Master | Rob O'Donnell | Yes | with Replay, co-pro, and probably GoMMC... |

| 51 | German B | Rob O'Donnell | Yes | (possible) May end up using this machine as Viewdata Station. |

| 60 | BBC Model B \#1 | Michael Firth | Yes | With RetroClinic DataCentre, for loading disk images via Econet |

| 61 | BBC Model B \#2 | Michael Firth | Yes | Pretty vanilla! |

| 62 | BBC Model B+ | Michael Firth | Yes | With RetroClinic IDE CF HD, plus ReCo6502 |

| 63 | BBC Master | Michael Firth | Yes | With RetroClinic IDE CF HD |

| 70 | Unknown | J.G.Harston | ?? | |

| 80-89 | Various | Joel Rowbottom | No | To be announced |

| 123 | Unknown | J.G.Harston | ?? | |

| 240 | A5000 (L4 server) | Rob O'Donnell | Yes | Viewdata BBS Server. |

| 245 | Archimedes A3020 (Server) | David Glover | Yes | Probably running awServer unless someone donates L4. Primarily serving 32-bit games and software. |

| 250 | Archimedes A3020 (Server) | Michael Firth | Yes | Will run L4 server, or awServer if re-serving an NFS drive from Linux. Has Ethernet interface too |

Changeable = "I'm happy to change ID if it clashes with something that is harder to change"

# AUN/Ethernet IP Addresses

Rob will be running a VoIP router to provide incoming telephone lines to the BBS. As a consequence of this, we will have a 'clean' subnet available at the show, NATted to the hotels network, should anybody have machines with ethernet interfaces that wishes to connect in. Please bring your own cables, and a hub/switch preferably with at least two more ports than you need to use (to allow us to daisy-chain them).

There will be a DHCP range (currently set to 192.168.15.150 - 199) for any ad-hoc machines that do not care about their address.

Static addresses can be used in the 192.168.15.x range. Assume that any entries in the Econet table above are already reserved.

Internet is there if you need it, but don't hog it - it'll be mainly for incoming connections to the viewdata BBS and/or econet. Not for catching up on your downloads :-)

Gateway is 192.168.15.1. DNS, unknown, depends on hotels ISP, but I'm using 208.67.222.222 / 208.67.220.220 (OpenDNS) which will work.

Under construction
