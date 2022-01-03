# Span\<T\> deck

**Created**: Thursday, December 20, 2018 05:12:47 AM -05:00
**Modified**: Monday, January 03, 2022 10:30:21 AM -05:00


**<span style="">From:</span>** <span style="">Felipe Pessoto</span><span style="">￼</span><span style="">Sent:</span> <span style="">Wednesday, December 19, 2018 7:57 PM</span><span style="">￼</span><span style="">To:</span> <span style="">Adam Sitnik; Mei-Chin Tsai; Rahul Agarwal; CLR Performance Discussions; WW Communities - Development; Jared Parsons</span><span style="">￼</span><span style="">Subject:</span> <span style="">RE: Span&lt;T&gt; deck</span>

<span style=""> </span>

<span style="">Wow, very good slides. Thanks Adam, your article is very helpful, as well (</span>[https://adamsitnik.com/Span/](https://nam06.safelinks.protection.outlook.com/?url=https%3A%2F%2Fadamsitnik.com%2FSpan%2F&amp;data=02%7C01%7CRobert.Bernstein%40microsoft.com%7C1b5ea8f6d8eb467a3b9108d6661624e3%7C72f988bf86f141af91ab2d7cd011db47%7C1%7C0%7C636808642768362879&amp;sdata=cj%2FKEk6mWIVyfjkt2c%2FGeVVwjGgpdfAePVmbMDRPvQw%3D&amp;reserved=0)<span style="">).</span>

<span style=""> </span>

<span style=""> </span>

**<span style="">From:</span>** <span style="">Adam Sitnik</span> &lt;Adam.Sitnik@microsoft.com<span style="">&gt;</span> <span style="">￼</span><span style="">Sent:</span> <span style="">Wednesday, December 19, 2018 7:11 PM</span><span style="">￼</span><span style="">To:</span> <span style="">Mei-Chin Tsai</span> &lt;meichint@microsoft.com<span style="">&gt;; Rahul Agarwal</span> &lt;rahulaga@microsoft.com<span style="">&gt;; Felipe Pessoto</span> &lt;felipe.pessoto@microsoft.com<span style="">&gt;; CLR Performance Discussions</span> &lt;clrperfe@microsoft.com<span style="">&gt;; WW Communities - Development</span> &lt;WWCDevelopment@service.microsoft.com<span style="">&gt;; Jared Parsons</span> &lt;jaredpar@microsoft.com<span style="">&gt;</span><span style="">￼</span><span style="">Subject:</span> <span style="">RE: Span&lt;T&gt; deck</span>

<span style=""> </span>

<span style="">I recently updated my slides about Span and gave a &quot;Spanification&quot; talk at</span> [Update Conference](https://nam06.safelinks.protection.outlook.com/?url=https%3A%2F%2Fwww.updateconference.net%2Fen%2Fsession%2Fspanification&amp;data=02%7C01%7CRobert.Bernstein%40microsoft.com%7C1b5ea8f6d8eb467a3b9108d6661624e3%7C72f988bf86f141af91ab2d7cd011db47%7C1%7C0%7C636808642768372887&amp;sdata=MZ0fAxzGcYtFYxEUGE6jHSvqF4Aqs3VuHFWOg5efJvQ%3D&amp;reserved=0) <span style="">in Prague.</span>

<span style=""> </span>

<span style="">The link:</span> [https://microsoft-my.sharepoint.com/:p:/p/adsitnik/Ef5XyNsgqzJErWZyu0x7XCEBQA6zKr2YtwwOO-WApx\_DXw?e=VuUQBu](https://nam06.safelinks.protection.outlook.com/?url=https%3A%2F%2Fmicrosoft-my.sharepoint.com%2F%3Ap%3A%2Fp%2Fadsitnik%2FEf5XyNsgqzJErWZyu0x7XCEBQA6zKr2YtwwOO-WApx_DXw%3Fe%3DVuUQBu&amp;data=02%7C01%7CRobert.Bernstein%40microsoft.com%7C1b5ea8f6d8eb467a3b9108d6661624e3%7C72f988bf86f141af91ab2d7cd011db47%7C1%7C0%7C636808642768372887&amp;sdata=KyBmOAriKzBXatj5SDAp1gCLzFgoJG16gbIlnLlZLfE%3D&amp;reserved=0)

<span style=""> </span>

<span lang="pl" style="">Content:</span>

1. <span lang="pl" style="">Introduction:</span>
    1. <span lang="en-US"><span lang="pl" style="">Managed heap</span></span>
    2. <span lang="en-US"><span lang="pl" style="">Unmanaged heap</span></span>
    3. <span lang="en-US"><span lang="pl" style="">Stack</span></span>
    4. <span lang="en-US"><span lang="pl" style="">Comparison</span></span>
2. <span lang="pl" style="">Span</span>
    1. <span lang="en-US"><span lang="pl" style="">What problem it solves</span></span>
    2. <span lang="en-US"><span style="">What is required to use it</span></span>
    3. <span lang="en-US"><span style="">API</span></span>
    4. <span lang="en-US"><span style="">ReadOnlySpan</span></span>
    5. <span lang="en-US"><span style="">How it works for the old and new runtimes</span></span>
    6. <span lang="en-US"><span style="">“Fast” vs “Slow” Span benchmarks</span></span>
3. <span style="">Spanification</span>
    1. <span lang="en-US"><span style="">Sample usage for parsing Utf8Strings using Utf8Parser</span></span>
    2. <span lang="en-US"><span style="">Reducing managed allocations by 72 GB to parse real 6.5GB ML.NET text file</span></span>
    3. <span lang="en-US"><span style="">MemoryExtensions</span></span>
    4. <span lang="en-US"><span style="">ArrayPool</span></span>
    5. <span lang="en-US"><span style="">Stack only:</span></span>

<span style="">                                                               </span><span style="">i.</span><span style="">      </span><span style="">What it means</span>

<span style="">                                                             </span><span style="">ii.</span><span style="">      </span><span style="">Memory</span>

<span style="">                                                           </span><span style="">iii.</span><span style="">      </span><span style="">How to use Memory and Span in async code</span>

<span style="">                                                           </span><span style="">iv.</span><span style="">      </span><span style="">How to write generic parser</span>

1. <span lang="en-US"><span style="">MemoryMarshal</span></span>

<span style=""> </span>

<span style="">Please let me know if something is not clear or does not work.</span>

<span style=""> </span>

<span style="">Thank,</span>

<span style="">Adam</span>

<span style=""> </span>

**<span style="">From:</span>** <span style="">Mei-Chin Tsai &lt;</span>meichint@microsoft.com<span style="">&gt;</span> <span style="">￼</span><span style="">Sent:</span> <span style="">Monday, December 17, 2018 11:59 PM</span><span style="">￼</span><span style="">To:</span> <span style="">Rahul Agarwal &lt;</span>rahulaga@microsoft.com<span style="">&gt;; Felipe Pessoto &lt;</span>felipe.pessoto@microsoft.com<span style="">&gt;; CLR Performance Discussions &lt;</span>clrperfe@microsoft.com<span style="">&gt;; WW Communities - Development &lt;</span>WWCDevelopment@service.microsoft.com<span style="">&gt;; Jared Parsons &lt;</span>jaredpar@microsoft.com<span style="">&gt;</span><span style="">￼</span><span style="">Subject:</span> <span style="">RE: Span&lt;T&gt; deck</span>

<span lang="pl" style=""> </span>

<span style="">Adding</span> [@Jared Parsons](mailto:jaredpar@microsoft.com) <span style="">who covered Span&lt;T&gt; in one of our recent presentation.</span>

<span style=""> </span>

<span style="">Thx,</span>

<span style="">Mei-Chin</span>

<span style=""> </span>

**<span style="">From:</span>** <span style="">Rahul Agarwal</span> <span style="">￼</span><span style="">Sent:</span> <span style="">Monday, December 17, 2018 6:19 AM</span><span style="">￼</span><span style="">To:</span> <span style="">Felipe Pessoto &lt;</span>felipe.pessoto@microsoft.com<span style="">&gt;; CLR Performance Discussions &lt;</span>clrperfe@microsoft.com<span style="">&gt;; WW Communities - Development &lt;</span>WWCDevelopment@service.microsoft.com<span style="">&gt;</span><span style="">￼</span><span style="">Subject:</span> <span style="">RE: Span&lt;T&gt; deck</span>

<span style=""> </span>

<span style="">Not sure if you have seen Adam Sitnik talk</span> [state of dot net performance](https://nam06.safelinks.protection.outlook.com/?url=https%3A%2F%2Fwww.youtube.com%2Fwatch%3Fv%3DCSPSvBeqJ9c&amp;data=02%7C01%7CRobert.Bernstein%40microsoft.com%7C1b5ea8f6d8eb467a3b9108d6661624e3%7C72f988bf86f141af91ab2d7cd011db47%7C1%7C0%7C636808642768382896&amp;sdata=fP06vruXdWc7brDYdPCcQ0fdUjAYItn7ZQY72M6Gkq8%3D&amp;reserved=0) <span style="">where he talked extensively about Span&lt;T&gt; and slides are available at</span> [https://www.slideshare.net/yuliafast/adam-sitnik-state-of-the-net-performance](https://nam06.safelinks.protection.outlook.com/?url=https%3A%2F%2Fwww.slideshare.net%2Fyuliafast%2Fadam-sitnik-state-of-the-net-performance&amp;data=02%7C01%7CRobert.Bernstein%40microsoft.com%7C1b5ea8f6d8eb467a3b9108d6661624e3%7C72f988bf86f141af91ab2d7cd011db47%7C1%7C0%7C636808642768392909&amp;sdata=S0F3%2FxolFq1kSGTNqRd8Fr93QaRKFa12bAXYDy7jQwk%3D&amp;reserved=0)

<span style=""> </span>

<span style="">Thanks!!</span>

<span style="">Rahul</span>

<span style=""> </span>

**<span style="">From:</span>** <span style="">Felipe Pessoto &lt;</span>felipe.pessoto@microsoft.com<span style="">&gt;</span> <span style="">￼</span><span style="">Sent:</span> <span style="">Monday, December 17, 2018 7:40 PM</span><span style="">￼</span><span style="">To:</span> <span style="">CLR Performance Discussions &lt;</span>clrperfe@microsoft.com<span style="">&gt;; WW Communities - Development &lt;</span>WWCDevelopment@service.microsoft.com<span style="">&gt;</span><span style="">￼</span><span style="">Subject:</span> <span style="">Span&lt;T&gt; deck</span>

<span style=""> </span>

<span style="">Hi everyone,</span>

<span style=""> </span>

<span style="">Does anybody have a PPT about Span&lt;T&gt;? An introduction, benefits, how it works, comparisons...</span>

<span style="">It is for an internal meeting where I would like to share this feature with my colleagues.</span>

<span style="">Thanks</span>