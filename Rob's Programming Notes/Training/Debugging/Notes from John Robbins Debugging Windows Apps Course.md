# Notes from John Robbins’ “Debugging Windows Apps” Course

**Created**: Tuesday, April 14, 2020 09:24:47 PM -04:00
**Modified**: Monday, January 03, 2022 10:30:21 AM -05:00


September 9th to 13th, 2002

# John Robbins’ Ten O’Clock Rules

10:01	Read “Code Complete” – John reads once a year, learns something new each time
10:02	Meet with your end users (at least once a month)
10:03	Get a cat for “Bug Talk”
10:04	Get a second computer – use PC # 1 to test bad case, PC # 2 to test normal case
10:05	Build with full symbols
10:06	If you must use STL, use stlport.org’s version of STL
10:07	Build at /W4, /WX (Warning Level 4, Treat Warnings As Errors)
10:08	Visit Sysinternals.com and get Process Explorer, other good tools
10:09	Check relocations, rebase.exe
10:10	Check all return values
10:11	Only use `_beginthreadex`
10:12	**<span style="text-decoration:underline">BANISH</span>** `CATCH(…)` from your whole life
10:13	Put all unit tests in version control and keep them updated
10:14	Set up and use a group-wide symbol server
10:15	Burn the daily build to CD
10:16	Get multiple monitors
10:17	Use `StrSafe.h` from Platform SDK
10:18	Install C RunTime Source Code
10:19	Check out https://www.microsoft.com/ddk/debugging
10:20	Read the WinDBG docs
10:21	Name all of your handle values (use unique names for unique process values)
10:22	**<span style="text-decoration:underline">BANISH</span>** `_set_se_translator` from your life
10:23	Set up a Master Build Machine
10:24	Buy SMP machines
10:25	Use `InitializeCriticalSectionAndSpinCount`.
10:26	Turn on the Debugging C Runtime
10:27	Ensure that you’re using the DLL version of the C RunTime
10:28	Have performance goals for your applications in your requirements documents

# John Robbins’ Recommended Books
1. “Code Complete” – Steve McConnell
2. “The C Programming Language” – Kernighan & Ritchie
3. “Debugging The Development Process” – Steve Maguire
4. “Managing The Testing Process” – Rex Black
5. “Don’t Make Me Think” – Steve Krug, UI Expert
6. “The Practice of Programming” – Kernighan & Pike
7. “Writing Secure Code”
8. “Inner Loops” – Rick Booth, Performance Expert
9. Scott Meyers’ books
10. “VB.NET and SQL Server” – Jimmy Nilsson, an eye-opener for Enterprise Apps
11. “Programming Apps for MS Windows, 4th Ed”, Jeffrey Richter
12. “Under Pressure and On Time” – Ed Sullivan

<hr />

**<span style="text-decoration:underline">When Creating A Schedule, Include Time To:</span>**

1.	Learn
2.	Design
3.	Implement
4.	Debug / Test
5.	Performance Tune

**<span style="text-decoration:underline">Scheduling Rules:</span>**

1.	Schedule development as a 30 hour work week, leaving time for meetings, etc.
2.	No task takes more than three days.  If it does, break it down into more tasks.
3.	The best project manager makes himself/herself irrelevant.

- Definition of a Bug – “Anything that causes a user pain”
- Plan Your Development – Don’t “Code First, Think Later”
- When debugging always have a hypothesis, never poke around
- The “Mythical Man Month” proved 30 years ago that adding people to a project does work to bring a product to market faster
- Once engineers admit what they don’t know, they can plan for learning

# The Debugging Process

![[Pasted image 20220103124140.png]]

From <https://d.docs.live.net/cadfae91c1651e6a/Documents/Debugging%20Windows%20Apps%20Notes.doc>

# Tools To Consider Evaluating:

## Regression Testing Utilities

1. Mercury WinRunner
2. Rational Visual Test (the best, in John’s opinion)
3. Microsoft’s App Center Test (ACT)

## Code Coverage Tools

1. NuMega CodeCoverage
2. bullseye.com’s Bullsit

## Version Control & BugTracking Tools

1. Starbase StarTeam (Both)
2. Perforce (Version Control) – used by NuMega, Intuit
3. Seapine (BugTracking) – Gives customer a tiny .exe to record errors
4. Incert Software’s TraceBack (BugTracking)
    1. eBay considered putting it on a production server!

- WDJ Magazine advertises all popular bug tracking systems
- **Ask each vendor for a live database that represents where you’ll be in 5 years.  If they can’t, eliminate them from the list.  This database should probably be at least 2 GB.**