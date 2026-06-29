---
layout: post
cover_color: #000000

keywords: EPLAN P8, EPLAN Automatic Page Elements

title: "EPLAN Page Elements"

description: >- 
  Each Automatic Page depend on page type there will be automatic placed elements inside pages such as cables, devices, PLC cards, etc. here in this post will list all Automatic Pages and their elements

date: 2024-03-10 10:00:00 +0800
author: Mahmoud Lotfi
file_name: 2024-01-04-eplan-page-2-elements-list.md
categories: [EPLAN, Page, Elements]
tags: [EPLAN, Page, Elements]
pin: False
math: true
mermaid: true
comments: true
toc: true
render_with_liquid: false

image:
  path: /assets/img/posts/eplan.jpg
  alt: EPLAN Page Elements
  lqip: data:image/webp;base64,UklGRjoAAABXRUJQVlA4IC4AAAA8AEAnQEqEAAIAAVAfCWkAALp8sF8rgRgAP7o9FDvMCkMde9PK7euH5M1m6VWoDXf2FkP3BqV0ZYbO6NA/VFIAAAA
---

# Automatic Page Elements

Each Automatic Page depend on page type there will be automatic placed elements inside pages such as cables, devices, PLC cards, etc. here in this post will list all Automatic Pages and their elements


## 1. Assembly/Module Overview `.f44`

### [Part](https://mlotfic.github.io/posts/eplan-page-3-automatic-pages-elements-01-part)

- Part
- Part (header object)
- Part reference
- Part reference (header object)
- Record

---

## 2. Cable assignment diagram `.f08`

### Cables

- Cable
- Cable part
- Cable part (assignment: source)
- Cable part (assignment: target)
- Cable part reference
- Cable part reference (assignment: source)
- Cable part reference (assignment: target)

### Device

- Device (source)
- Device (target)

### Part

- Part (source)
- Part (target)
- Part reference (source)
- Part reference (target)
- Record

### PCT (Physical Connection Technology)

- PCT loop (`stand for Physical Connection Technology`)  
- PCT loop function

### Pre-planning

- Pre-planning segment

---

## 3. Cable diagram `.f09`

### Cable

- Cable
- Cable part
- Cable part (assignment: source)
- Cable part (assignment: target)
- Cable part reference
- Cable part reference (assignment: source)
- Cable part reference (assignment: target)

### Connection

- Cable connection
- Connection part
- Connection part (assignment: source)
- Connection part (assignment: target)
- Connection part reference
- Connection part reference (assignment: source)
- Connection part reference (assignment: target)

### Device

- Device (source)
- Device (target)

### Part

- Part (source)
- Part (target)
- Part reference (source)
- Part reference (target)
- Record

### PCT (Physical Connection Technology)

- PCT loop
- PCT loop function

### Pre-planning

- Pre-planning segment

---

## 4. Cable overview `.f10`

### Cable

- Cable
- Cable part
- Cable part (assignment: source)
- Cable part (assignment: target)
- Cable part reference
- Cable part reference (assignment: source)
- Cable part reference (assignment: target)

### Device

- Device (source)
- Device (target)

### Part

- Part (source)
- Part (target)
- Part reference (source)
- Part reference (target)
- Record

### PCT (Physical Connection Technology)

- PCT loop
- PCT loop function

### Pre-planning

- Pre-planning segment

---

## 5. Cable-connection diagram `.f07`

### Cable

- Cable
- Cable connection
- Cable part
- Cable part (assignment: source)
- Cable part (assignment: target)
- Cable part reference
- Cable part reference (assignment: source)
- Cable part reference (assignment: target)
- Cable, external 'level (1-3)'
- Cable, internal 'level (1-3)'

### Connection

- Connection, external 'level (1-3)'
- Connection, internal 'level (1-3)'
- Last external target
- Last internal target

- PCT loop
- PCT loop function
- Pre-planning segment

- Target, external 'level (1-3)'
- Target, external, connection point 'level (1-3)'
- Target, external, counter-connection 'level (1-3)'
- Target, internal 'level (1-3)'
- Target, internal, connection point 'level (1-3)'
- Target, internal, counter-connection 'level (1-3)'

---

## 6. Conduit / line plan `.f46`

- Conduit / line

- Connection

- Connection part
- Connection part reference

- Device (source)
- Device (target)

- Part
- Part reference

- PCT loop
- PCT loop function
- Pre-planning segment
- Record

---

## 7. Connection List `.f27`

- 3D part placement (source)
- 3D part placement (target)

- Cable
- Cable unit
- Cable unit part
- Cable unit part reference

- Connection

- Connection part
- Connection part (assignment: source)
- Connection part (assignment: target)
- Connection part reference
- Connection part reference (assignment: source)
- Connection part reference (assignment: target)

- Device (source)
- Device (target)

- Part (source)
- Part (target)
- Part reference (source)
- Part reference (target)

- Record

- Wire harness
- Wire harness part
- Wire harness part reference

---

## 8. Cut-out legend `.f47`

- 3D model view
- Cut-out
- Record

---

## 09. Device tag list `.f03`

- Device group (further functions)
- Device tag
- Function
- Part
- Part reference
- PCT loop
- PCT loop function
- Pre-planning segment
- Record

- Connected PLC connection point

---

## 10. Device-connection diagram `.f05`

- Cable, external 'level (1-3)'
- Cable, internal 'level (1-3)'
- Connected PLC connection point
- Connection point, external
- Connection point, internal
- Connection, external 'level (1-3)'
- Connection, internal 'level (1-3)'
- Device
- Function
- Last external target
- Last internal target

- Part
- Part reference

- PCT loop
- PCT loop function

- Pre-planning segment

- Target, external 'level (1-3)'
- Target, external, connection point 'level (1-3)'
- Target, external, counter-connection 'level (1-3)'
- Target, internal 'level (1-3)'
- Target, internal, connection point 'level (1-3)'
- Target, internal, counter-connection 'level (1-3)'

---

## 11. Distributed device list `.f45`

- Device tag
- Function
- Part
- Part reference
- Record

---

## 12. Enclosure legend `.f18`

- 3D model view
- Device
- Mounting panel
- Mounting panel part
- Mounting panel part reference
- Part
- Part placement
- Part reference
- Record

---

## 13. Forms documentation `.f04`

- Form
- Record

---

## 14. Manufacturer / supplier list `.f31`

- Manufacturer / supplier
- Record

---

## 15. Mounting list `.f32`

### Device

- Device
- Device (header object)

### Part

- Part
- Part (header object)
- Part placement
- Part placement (header object)
- Part reference
- Part reference (header object)
- Record

---

## 16. P&I diagram: Piping overview `.f37`

- Device
- Device (source)
- Device (target)
- PCT loop
- PCT loop function
- Pipe class
- Piping
- Piping planning object
- Record
- Substance

---

## 17. Parts list `.f01`

- Device
- Mounting panel
- Part placement
- Part reference
- Part reference manufacturer
- Part reference supplier
- PCT loop
- PCT loop function
- Pre-planning segment
- Record
Part


---

## 18. Pin-connection diagram `.f21`

Cable, external 'level (1-3)'
Cable, internal 'level (1-3)'
Connected PLC connection point
Connection, external 'level (1-3)'
Connection, internal 'level (1-3)'
Last external target
Last internal target
Part
Part reference
PCT loop
PCT loop function
Pin
Plug
Plug counterpiece
Pre-planning segment
Target, external 'level (1-3)'
Target, external, connection point 'level (1-3)'
Target, external, counter-connection 'level (1-3)'
Target, internal 'level (1-3)'
Target, internal, connection point 'level (1-3)'
Target, internal, counter-connection 'level (1-3)'

---

19. Placeholder object overview `.f30`

Device
Page
Placeholder object
Record
Value set table

---

20. PLC address overview `.f48`

PCT loop
PCT loop function
PLC addresses
PLC connection point
Pre-planning segment
Record

---

21. PLC card overview `.f20`

Connected sensor / actuator per connection point
Part
Part reference
PCT loop
PCT loop function
PLC card
PLC card communication unit
PLC connection point
Pre-planning segment
Record


---

22. PLC diagram `.f19`

Connected sensor / actuator
Connection
Connection / cable
Part
Part reference
PCT loop
PCT loop (header object)
PCT loop function
PCT loop function (header object)
PLC card
PLC card communication unit
PLC connection point
Pre-planning segment
Pre-planning segment (header object)
Record
Target

---

23. Plot frame documentation `.f15`

Plot frame
Record

---

24. Plug diagram `.f22`
Cable chart data area external
Cable chart data area internal
Cable chart data area via form position
Cable chart header
Cable chart header external
Cable chart header external: Counter target
Cable chart header internal
Cable chart header internal: Counter target
Cable chart header via form position
Cable chart header: Counter target
Connected PLC connection point
Connection / cable external
Connection / cable internal
Connection / cable via form position
Connection via form position
Connection, external
Connection, internal
Female pin end
Female pin end: Cable chart data area
Female pin end: Connected PLC connection point
Female pin end: Connection
Female pin end: Connection / cable
Female pin end: Pin
Female pin end: Pin part
Female pin end: Pin part reference
Female pin end: Plug part
Female pin end: Plug part reference
Female pin end: Target
Male pin end
Male pin end: Cable chart data area
Male pin end: Connected PLC connection point
Male pin end: Connection
Male pin end: Connection / cable
Male pin end: Pin
Male pin end: Pin part
Male pin end: Pin part reference
Male pin end: Plug part
Male pin end: Plug part reference
Male pin end: Target
PCT loop
PCT loop function
Pin
Pin part
Pin part reference
Plug
Plug part
Plug part reference
Pre-planning segment
Record
Target external
Target internal
Target via form position

---

25. Plug overview `.f23`
Part
Part reference
PCT loop
PCT loop function
Plug
Plug counterpiece
Pre-planning segment
Record
Target external
Target internal

---

26. Potential overview `.f16`
Potential
Record

---

27. Preplanning: Pipe class overview `.f49`
Pipe class
Record

---

28. Pre-planning: Planning object overview `.f40`
Cable planning object
Device
Function
Linked segments
Linked with superior segments
Page
Part
Part reference
PCT loop
PCT loop function
Pipe class
Piping definition
Piping planning object
Placement P&I diagram
Placement pre-planning
Planning object
PLC addresses
Record
Source segment
Structure segment hierarchical
Subordinate segment
Substance
Superior segment
Superior structure segment
Target segment


---

29. Pre-planning: Planning object plan `.f41`
Device
Device (header object)
Function
Function (header object)
Linked segments
Linked with superior segments
Page
Part
Part (header object)
Part reference
Part reference (header object)
PCT loop (header object)
PCT loop function (header object)
Pipe class (header object)
Piping definition
Piping definition (header object)
Piping planning object
Piping planning object (header object)
Placement P&I diagram
Placement P&I diagram (header object)
Placement pre-planning
Placement pre-planning (header object)
Planning object
Planning object (header object)
PLC addresses
PLC addresses (header object)
Record
Source segment
Source segment (header object)
Structure segment hierarchical
Substance (header object)
Superior segment (header object)
Target segment
Target segment (header object)

---

30. Pre-planning: Segment template overview `.f42`
Part
Record
Segment template

---
31. Pre-planning: Segment template plan `.f43`
Device
Function
Part
Part reference
Planning object
PLC addresses
Record
Segment template

---

32. Pre-planning: Structure segment overview `.f38`
Linked segments
Linked with superior segments
Page
Placement pre-planning
Record
Structure segment
Structure segment hierarchical

---

33. Pre-planning: Structure segment plan `.f39`
Device
Function
Linked segments
Linked with superior segments
Page
Part
Part reference
Placement P&I diagram
Placement pre-planning
Placement pre-planning (header object)
PLC addresses
Record
Structure segment (header object)
Structure segment / Planning object
Structure segment hierarchical

---

34. Preplanning: Substance overview `.f51`

Record
Substance

---

35. Project options overview `.f29`

Placeholder object
Project option
Project option section
Record

---

36. Revision overview `.f17`

Page
Project
Record


---

37. Structure identifier overview `.f24`

Document type
Function designation
Functional assignment
Installation site
Location designation
Product
Record
Structure identifier
User-defined structure
Higher-level function number

---

38. Summarized parts list `.f02`

Device
Mounting panel
Part
Part placement
Part reference
Part reference manufacturer
Part reference supplier
PCT loop
PCT loop function
Pre-planning segment
Record

---

39. Symbol overview `.f25`

Record
Symbol
Symbol library
Variants (all variants)


---

40. Table of contents `.f06`

Page
PCT loop
PCT loop function
Pre-planning segment
Project
Record



---

41. Terminal diagram `.f13`

Cable chart data area external
Cable chart data area internal
Cable chart data area via connection point
Cable chart data area via form position
Cable chart header
Cable chart header external
Cable chart header external: Counter target
Cable chart header internal
Cable chart header internal: Counter target
Cable chart header via connection point
Cable chart header via form position
Cable chart header: Counter target
Connected PLC connection point
Connection / cable external
Connection / cable internal
Connection / cable via connection point
Connection / cable via form position
Connection via connection point
Connection via form position
Connection, external
Connection, internal
Main terminal
Main terminal part
Main terminal part reference
PCT loop
PCT loop function
Pre-planning segment
Record
Target external
Target internal
Target via connection point
Target via form position
Terminal
Terminal connection point external
Terminal connection point internal
Terminal part reference
Terminal parts
Terminal strip
Terminal strip part reference
Terminal strip parts

---

42. Terminal line-up diagram `.f12`

PCT loop
PCT loop function
Pre-planning segment
Terminal
Terminal part reference
Terminal part reference by product subgroups
Terminal parts
Terminal parts by product subgroups
Terminal strip
Terminal strip part reference
Terminal strip part reference by product subgroups
Terminal strip parts
Terminal strip parts by product subgroups


---
43. Terminal-connection diagram `.f11`

Cable, external 'level (1-3)'
Cable, internal 'level (1-3)'
Connected PLC connection point
Connection, external 'level (1-3)'
Connection, internal 'level (1-3)'
Last external target
Last internal target
PCT loop
PCT loop function
Pre-planning segment
Target, external 'level (1-3)'
Target, external, connection point 'level (1-3)'
Target, external, counter-connection 'level (1-3)'
Target, internal 'level (1-3)'
Target, internal, connection point 'level (1-3)'
Target, internal, counter-connection 'level (1-3)'
Terminal
Terminal connection point external
Terminal connection point internal
Terminal part reference
Terminal parts
Terminal strip
Terminal strip part reference
Terminal strip parts

---

44. Terminal-strip overview `.f14`

PCT loop
PCT loop function
Pre-planning segment
Record
Target external
Target internal
Terminal strip
Terminal strip part reference
Terminal strip parts

---

45. Topology: Routed cables / connections `.f36`

Cable / connection
Cable / Connection part
Cable / Connection part (assignment: source)
Cable / Connection part (assignment: target)
Cable / Connection part reference
Cable / Connection part reference (assignment: source)
Cable / Connection part reference (assignment: target)
Device (source)
Device (target)
Part (target)
Part reference (source)
Part reference (target)
Part (source)

---

46. Topology: Routing path diagram `.f35`

Cable / connection
Cable / Connection part
Cable / Connection part (assignment: source)
Cable / Connection part (assignment: target)
Cable / Connection part reference
Cable / Connection part reference (assignment: source)
Cable / Connection part reference (assignment: target)
Device (source)
Device (target)
Routing path (topology)
Routing path part (topology)
Routing path part reference (topology)

---

47. Topology: Routing path list `.f34`

Device (source)
Device (target)
Part (source)
Part (target)
Part reference (source)
Part reference (target)
Record
Routing path (topology)
Routing path part (topology)
Routing path part reference (topology)

---