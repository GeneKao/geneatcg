---
title: "Swarm Python Component"
date: 2014-06-25
tags: ["python", "programming", "design", "rhino-grasshopper"]
description: "Swarm in Grasshopper using GH_Python component."
---

Swarm in Grasshopper using GH_Python component. Testing swarm behaviour in Rhino is in this post: Rhino.Python Swarm Bridge

<iframe width="100%" height="450" src="//www.youtube.com/embed/uNO9LP2Yy_M" frameborder="0" allowfullscreen></iframe>

For more discussion please visit my post in [grasshopper example forum](https://www.grasshopper3d.com/forum/topics/swarm-example-component-using-python-timer).


### GH_Python Code:

``` python
### --Written by Gene Ting-Chun Kao-- ###
ghenv.Component.Message = "written by +GENEATCG"

import rhinoscriptsyntax as rs
import Rhino as rc
from random import *

rectX = 600
rectY = 600

class Runner:
    def __init__(self, p, v):
        self.p = p
        self.v = v
        self.a = rs.VectorCreate( (0,0,0),(0,0,0) )

    def ptRun(self):
        self.v = rs.VectorAdd(self.v, self.a)
        v = rs.VectorLength(self.v)
        if v > 2:
            self.v = rs.VectorScale(rs.VectorUnitize(self.v), 2)
        self.p = rs.VectorAdd(self.p, self.v)

        self.a = rs.VectorCreate( (0,0,0),(0,0,0) )

    # ... (full code on GitHub)
```
