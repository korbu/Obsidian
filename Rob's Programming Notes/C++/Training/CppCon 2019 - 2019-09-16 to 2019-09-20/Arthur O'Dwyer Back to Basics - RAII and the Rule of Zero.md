# Arthur O'Dwyer: "Back to Basics - RAII and the Rule of Zero"

**Created**: Monday, November 04, 2019 12:29:37 PM -05:00
**Modified**: Monday, November 04, 2019 01:12:48 PM -05:00

1. Day Two - 09/17/2019
2. Resource Acquisition Is Initialization (RAII)
3. ![](/Attachments/1-d51c195fadab4dd2ba4b890ee610d4b4.png)

4. ![](/Attachments/1-3c8f32a75358434c83bb72f52de64f38.png)

5. ![](/Attachments/1-003ee27a3fee456faef2812e395f5af2.png)

6. ![](/Attachments/1-de3a3c3bd4ca4ba2914921e6f7627c14.png)

7. ![](/Attachments/1-d02a13f662694be7aaa6832a8ad84533.png)

8. ![](/Attachments/1-c500c9b06f524eadace137f6dbe2c173.png)

9. ![](/Attachments/1-dd16df55615a4221af50d2092a32f42b.png)

10. ![](/Attachments/1-aba5bf26332242dcba730967c161bd68.png)

11. ![](/Attachments/1-af63ca5171fe4078a1378b5621f2f820.png)

12. ![](/Attachments/1-fdbdede48db24b7db677f14088393f9b.png)
    1. <mark style="background: #BBFABBA6;">If you write a destructor, you need to write a copy constructor.</mark>
13. ![](/Attachments/1-c2c2f2148fd445f2bb6af06d83b89480.png)
    1. <mark style="background: #BBFABBA6;">This slide is super-important.</mark>
    2. <mark style="background: #BBFABBA6;">This trips up a lot of people.</mark>
    3. <mark style="background: #BBFABBA6;">This will call the default copy constructor if you don't explicitly provide one, which simply copies each member, including the pointer to the dynamically allocated memory.</mark>
    4. <mark style="background: #BBFABBA6;">Remember this!</mark>
14. ![](/Attachments/1-c05f419f641d40afac065d25ebb95a7d.png)
    1. <mark style="background: #BBFABBA6;">Generates an implicit = operator which copy-assigns each member.</mark>
15. ![](/Attachments/1-baf07cff57c14dd2a66a2db0877b70bc.png)
    1. <mark style="background: #BBFABBA6;">Whenever you write a destructor, you (probably) need to write a copy constructor <strong><span style="">and a copy assignment operator</span></strong>.</mark>
    2. He recommends that you cheat a little.
    3. Don't write all of that manual management by hand.
    4. <mark style="background: #BBFABBA6;">He's going to write the copy assignment operator in terms of the copy constructor and a swap member function.</mark>
    5. Note that we haven't written the swap member function yet.
        1. Swap the pointers.
        2. Swap the sizes.
        3. <mark style="background: #FFF3A3A6;">It can (must?) be noexcept.</mark>
16. ![](/Attachments/1-d136d44f81e44d418c73646fd8721360.png)

17. ![](/Attachments/1-c57077934b544f419a97b8720c869936.png)
    1. He is using the wrong kind of delete here.
    2. <mark style="background: #BBFABBA6;">It should be delete [] ptr_;</mark>
    3. Remember that ptr\_ and size\_ are class member variables.
18. Now assign v = w.
19. ![](/Attachments/1-9ecf686485914e86a40ca9e9f167736a.png)

20. ![](/Attachments/1-88d37f3d1454477581b923ba3e43795a.png)

21. ![](/Attachments/1-1bc821d6b6064a7d808783f1029be32a.png)
22. No problems until someone says v = v.
23. ![](/Attachments/1-979f637413f640568d176e19336c2e40.png)
24. `v` is a `const` reference to itself.
25. ![](/Attachments/1-bb20a8ca74374e0d8e3e0fcd2f5819ad.png)

26. ![](/Attachments/1-88821b0ba7774ea6920f25b22ff80a8d.png)

27. ![](/Attachments/1-21a93d15a2614a67ba666b2deefd1c3b.png)
28. <mark style="background: #BBFABBA6;">Self-copy is a problem.</mark>
29. ![](/Attachments/1-07a1f7377be24a36be5b433ee6a7d1e7.png)
30. Stopped at 14:12 in the video b/c my Bluetooth headphones ran out of battery.
