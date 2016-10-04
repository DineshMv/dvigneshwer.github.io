---
layout: post
title: "Installing GG plot"
date: 2016-05-11
---

# Tutorial for installing ggplot

* ggplot is a python module which helps in visualizing of plots etc

~~~~
pip install ggplot
~~~~

This requires $DISPLAY variable so make when you ssh into a machine for installing 

~~~~
ssh -X server_name@ip_addr
~~~~

Other packages it needs are,

~~~~
apt-get install python3-tk
~~~~

if you are checking via ipython, make sure import mathplotlib

~~~~
import mathplotlib

mathplotlib.use('Agg')

import ggplot
~~~~
