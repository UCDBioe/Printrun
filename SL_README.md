To Run
======
conda environment: bioprint
pythonw pronterface.py

To Build with py2app
====================
* To make a setup.py file: `py2applet --make-setup pronterface.py`
* To build: `pythonw setup.py py2app -A`
  * The `-A` makes it a local distribution, remove to make it deployable 

Heat Buttons
------------
* gui.py: line 90 - static text "Heat"
* Bound to method: root.htemp_change
* pronterface.py -> htemp_change
  * line 595
* pronterface.py -> do_settemp
  * `def do_settemp(self, l = ""):`
  * pronterface line 344
  * command sent:
    * `self.p.send_now("M104 S"+l)`


Bed Buttons
-----------
* gui.py: line 109 - static text "Bed"  
* Bound to method: root.btemp_change
* pronterface.py -> btemp_change
  * line 600
* pronterface.py -> do_bedtemp
  * `def do_settemp(self, l = ""):`
  * pronterface line 364
  * command sent:
    * `self.p.send_now("M140 S"+l)`

Extrude Button
--------------
* SpecialButton
* pronsole.py -> do_extrude
    * `def do_extrude(self, l, override = None, overridefeed = 300):`
    * pronsole.py, line 998
    * method to extrude filament
    * Commands sent to execute:
    * `` 
        self.p.send_now("G91")
        self.p.send_now("G1 E"+str(length)+" F"+str(feed))
        self.p.send_now("G90")
      ``

Add Buttons
===========
* `printrun/gui.py - make_sized_button - make_button`
* `def make_button(parent, label, callback, tooltip, container = None, size = wx.DefaultSize, style = 0):`
* `root.printbtn = make_sized_button(root.panel, _("Print"), root.printfile, _("Start Printing Loaded File"), self)`
* Special Button
  *  printrun/pronterface_widgets.py -  
  *  `def __init__(self, label, command, background = None, pos = None, span = None, tooltip = None, custom = False):`
UV_LED
------
* `root.uvledbtn = make_sized_button(root.panel, _("UV LED"), root.uvled, _("Toggle UV LED"), self)`
* `root.uvledbtn = make_sized_toggle_button(root.panel, _("UV LED"), root.uvled, _("Toggle UV LED"), (6,0))`
* `def uvled(self, event):`
