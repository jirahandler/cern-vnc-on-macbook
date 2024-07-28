# CERN VNC on MacBook

This repo has instructions to use VNC with RHEL9 like machines.

# `vnc` using `systemd`

This one is with the `systemd` recipe.

On your local computer, either do `kinit` if you have right settings for EL9, or use Ticket Viewer GUI (Macs only) to obtain an lxplus kerberos ticket.

```
###### Your local computer ###################
[mySkynet ~] ssh hepbro@lxplus.cern.ch

#########The following is on lxplus#############

[hepbro@lxplus9XY ~]  loginctl enable-linger
[hepbro@lxplus9XY ~]  systemd-run --scope --user screen

######This goes inside screen session##################

[hepbro@lxplus9XY ~]  UIID=`id -u`
[hepbro@lxplus9XY ~]  VNC_DISPLAY=$(( 1 + UIID % 65535))
[hepbro@lxplus9XY ~]  VNC_PORT=$((VNC_DISPLAY + 5900)) # for your reference
[hepbro@lxplus9XY ~]  systemctl --user start vncserver@${VNC_DISPLAY}.service
[hepbro@lxplus9XY ~]  CTRL + A (^A) and then CTRL + D (^D)
```
Then on your local skynet computer terminal:

```
[mySkynet ~] ssh -L <VNC_PORT>:localhost:<VNC_PORT> hepbro@lxplus9XY.cern.ch
# where hepbro= Your CERN username, & XY is a set of 2 digits, may be more
```
