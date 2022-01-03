# Typings

**Created**: Thursday, May 04, 2017 01:14:09 PM -04:00
**Modified**: Monday, January 03, 2022 10:30:18 AM -05:00


<span style="background-color:white">Typings: The TypeScript Definition Manager.</span>

*<span style="">#&#160;Install&#160;Typings&#160;CLI&#160;utility.&#160;</span>*

<span style="">npm&#160;install&#160;typings&#160;--global</span>

<span style="">&#160;</span>

*<span style="">#&#160;Search&#160;for&#160;definitions.&#160;</span>*

<span style="">typings&#160;search&#160;tape</span>

<span style="">&#160;</span>

*<span style="">#&#160;Find&#160;a&#160;definition&#160;by&#160;name.&#160;</span>*

<span style="">typings&#160;search&#160;--name&#160;react</span>

<span style="">&#160;</span>

*<span style="">#&#160;If&#160;you&#160;use&#160;the&#160;package&#160;as&#160;a&#160;module:&#160;</span>*

*<span style="">#&#160;Install&#160;non-global&#160;typings&#160;(defaults&#160;to&#160;&quot;npm&quot;&#160;source,&#160;configurable&#160;through&#160;`defaultSource`&#160;in&#160;`.typingsrc`).&#160;</span>*

<span style="">typings&#160;install&#160;debug&#160;--save</span>

<span style="">&#160;</span>

*<span style="">#&#160;If&#160;you&#160;use&#160;the&#160;package&#160;through&#160;`&lt;script&gt;`,&#160;it&#160;is&#160;part&#160;of&#160;the&#160;environment,&#160;or&#160;</span>*

*<span style="">#&#160;the&#160;module&#160;typings&#160;are&#160;not&#160;yet&#160;available,&#160;try&#160;searching&#160;and&#160;installing&#160;with&#160;`--global`:&#160;</span>*

<span style="">typings&#160;install&#160;dt~mocha&#160;--global&#160;--save</span>

<span style="">&#160;</span>

*<span style="">#&#160;If&#160;you&#160;need&#160;a&#160;specific&#160;commit&#160;from&#160;github.&#160;</span>*

<span style="">typings&#160;install&#160;d3=github:DefinitelyTyped/DefinitelyTyped/d3/d3.d.ts#1c05872e7811235f43780b8b596bfd26fe8e7760&#160;--global&#160;--save</span>

<span style="">&#160;</span>

*<span style="">#&#160;Search&#160;and&#160;install&#160;by&#160;version.&#160;</span>*

<span style="">typings&#160;info&#160;env~node&#160;--versions</span>

<span style="">typings&#160;install&#160;env~node@0.10&#160;--global&#160;--save</span>

<span style="">&#160;</span>

*<span style="">#&#160;Install&#160;typings&#160;from&#160;a&#160;particular&#160;source&#160;(use&#160;`&lt;source&gt;~&lt;name&gt;`&#160;or&#160;`--source&#160;&lt;source&gt;`).&#160;</span>*

<span style="">typings&#160;install&#160;env~atom&#160;--global&#160;--save</span>

<span style="">typings&#160;install&#160;bluebird&#160;--source&#160;npm&#160;--save</span>

<span style="">&#160;</span>

*<span style="">#&#160;Use&#160;`typings/index.d.ts`&#160;(in&#160;`tsconfig.json`&#160;or&#160;as&#160;a&#160;`///`&#160;reference).&#160;</span>*

<span style="">cat&#160;typings/index.d.ts</span>

From &lt;https://www.npmjs.com/package/typings&gt;