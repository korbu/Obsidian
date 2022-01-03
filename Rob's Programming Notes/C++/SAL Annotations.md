# SAL Annotations

**Created**: Friday, January 22, 2021 03:27:54 PM -05:00
**Modified**: Friday, January 22, 2021 03:42:58 PM -05:00


# References

1. Nico's PPT: [XStore OACR.pptx (sharepoint.com)](https://microsoft.sharepoint.com/:p:/t/AzureStorage/EWg-LPQwOZBBgdgCZplwwhABv5CjZ1wX5NU7jBF5FD00Dw?e=X1CFcb) (see screenshots from it, below)

2. xstoreoacr@microsoft.com - XStore OACR contacts​
3. oacrsig@microsoft.com - OACR Special Interest Group – Discussion Alias​

    ​
4. http://oacrhelp/​
5. [OACR OneNote](https://microsoft.sharepoint.com/teams/OACR/Shared%20Documents/OACR%20Documentation?Web=1)​

    ​
6. XStore wiki (rather limited currently): https://microsoft.sharepoint.com/teams/AzureStorage/Dev%20Wiki/OACR.aspx​
7. Office wiki: https://www.owiki.ms/wiki/OACR​
8. OSG wiki: [https://osgwiki.com/wiki/Windows\_Static\_Analysis\_FAQ](https://osgwiki.com/wiki/Windows_Static_Analysis_FAQ)​
9. SAL 1-&gt;2 conversion table: http://windowstoolsarchive/analysis/SAL/SAL%201%20to%20SAL%202%20Conversion%20Table.xlsx​

![SAL primitives
Property
Validity
Const-ness
NULL termination
Null-ness
Buffer size
Annotations
Valid
Notvalid
Const
Null terminated
Null
Notnull
_ Maybenull_
_ Readable_elements_(size)
_ Writable_elements_(size)
_ Readable_bytes_(size)
_ Writable_bytes_(size) ](/Attachments/1-3da7cda95a330ec6a64ec1392525e645.png)
![High level macros combine primitives
into common scenarios
Input parameter
Pointer to initialized buffer on entry
Buffer is not modified by function
OUtPUt parameter
Pointer to uninitialized buffer on entry
Buffer is filled by function
Input/output parameter
Pointer to initialized buffer on entry
Buffer is modified by function
OUtPUt pointers (including pointer to references)
Pointer to output parameter (see above) ](/Attachments/1-eb2dff47c77009e2872be3c9225610e6.png)
![SAL 2
Input Buffers
_in_opt
In z
reads_(size)
In
ln_opt_
ln_opt_z_
In
reads_opt_(size)
In
reads_z_(size)
In
reads_or_z_(size)
In
reads_opt_z_(size)
In
reads_bytes_(size)
In
reads_bytes_opt_(size)
In
Windows SAL 1
in
in
z
in_z_opt
in_ecount(size)
_in_ecount_opt(size)
in_ecount_z(size)
in_ecount_or_z(size)
in_ecount_z_opt(size)
in_bcount(size)
_in_bcount_opt(size) ](/Attachments/1-15c73b280f2303a4a1f5b1b1a6dc09de.png)
![In
Parameter must be valid in pre state and will not be modified
Function will only read from the single-element buffer
Call must provide the buffer and initialize it
Pretty much implies const.
Example
void Get Info (
In
In
In
PCWCHAR pch,
PCWSTR pName,
int num
points to a single WCHAR
input only
points to null—terminated string on
input, won&#39;t be written to
no—op for scalar ](/Attachments/1-1c98db2b44f20ce1aa139ebfba2c51a1.png)
![ln_opt_
Same as _ln_, except the parameter may be null
_opt_ is always a precondition (parameter at function entry)
Not to be used for parameters with default values.
Example
HANDLE WINAPI createFi1e (
In
In
In
In
In
In
In
LPCTSTR IpFi1eName,
DWORD dwDesiredAccess,
DWORD dwShareMode,
opt LPSECURITY ATTRIBUTES IpsecurityAttributes,
DWORD dwCreationDisposition,
DWORD dwF1agsAndAttributes,
opt HANDLE hTempIateFi1e) ; ](/Attachments/1-32a8f86ffed50ec0b078145a7277db51.png)
![ln_reads_(n)
ln_reads_bytes_(n)
Used to annotate a pointer to array which is read by the function
Array is of size n elements, all of which must be valid
_bytes_ form gives the size in bytes rather than elements
Example
int main (
In int argc,
In reads (argc) LPWSTR *argv) ;
void * memcpy (
Out writes bytes (size) char *dest,
In reads bytes (size) char *src,
In int size); ](/Attachments/1-3d08fef010a10797b7e6a0f5affe4c4c.png)
![ln_reads_opt_(n)
ln_reads_bytes_opt_(n)
Same as _ln_reads_/_ln_reads_bytes_, except the parameter may be null
Example
HRESULT SessionOption (
In reads_opt (dwLen) long *pBuf ,
DWORD dwLen) ;
HRESULT Ur1MkSetSessionOption (
DWORD dwOption,
In (dwBufferLength) LPVOID pBuffer ,
DWORD dwBufferLength,
Reserved DWORD dwReserved ](/Attachments/1-15e6b1d0844803738796bd860427a256.png)
![In z
Applied to annotate a pointer to a null terminated string
The string must be valid in pre-state
Example
int ReadString (
In z const char string) ; ](/Attachments/1-9b4a3f1f92a90766acc41ed642d6a656.png)
![SAL 2
Out
Out writes_(size)
out
writes_z_(size)
out
writes_bytes_(size)
Out writes_bytes_opt_(size)
Out writes_to_(size, count)
out
writes_bytes_to_(size, count)
OUtPUt Buffers
Out opt
out opt
Out writes_opt_(size)
Out writes_opt_z_(size)
Windows SAL 1
out
out_ecount(size)
out_ecount_opt(size)
out_ecount_z(size)
out_ecount_z_opt(size)
out_bcount(size)
out_bcount_opt(size)
out_ecount_part(size, count)
out_bcount_part(size, count) ](/Attachments/1-fa72e3b5fd950f98bf5d748127f80c86.png)
![Out
The parameter needs not be valid in pre state and must be valid in post state
The single-element buffer will be filled by the function
The caller must provide the buffer and the function will initialize it
Example
Success (return >= 0 )
int Write(
Out PWCHAR pch / / points to a single WCHAR
// output only ](/Attachments/1-e408a9f1b64a06da9a9ca599704763e2.png)
![_ Out_writes_(n)
Out_writes_bytes_(n)
Used to annotate a pointer to an array of n elements that will be written by the
function
Specifies the caller provides a buffer and the function initializes it
Does not indicate how many elements the function writes to the buffer
Example
void WriteToBuf (
Out
Out
Out
size
writes (num) wchar t *bufl ,
writes (num) LPWSTR buf2,
writes all (num) wchar t *buf3,
t num) ; ](/Attachments/1-cbc25a81edea0b129036099abc5f7844.png)
![SAL 2
Inout
Inout opt
Inout z
Inout_opt_z_
Inout_updates_(size)
Inout_updates_opt_(size)
Inout_updates_z_(size)
Inout_updates_opt_z_(size)
Inout_updates_bytes_(size)
Inout_updates_bytes_opt_(size)
Inout_updates_bytes_to_(size, count)
Input/outPUt Buffers
inout_z_opt
Inout_updates_to_(size, count)
Windows SAL 1
inout
inout_opt
inout
z
inout_ecount(size)
inout_ecount_opt(size)
inout_ecount_z(size)
inout_ecount_z_opt(size)
inout_bcount(size)
inout_bcount_opt(size)
inout_ecount_part(size, count)
inout_bcount_part(size, count) ](/Attachments/1-149df92c7a7507a4bf66ef382890e110.png)
![Inou.Jt
Used to annotate a parameter that will be changed by the function
Must be valid in both pre and post states
The caller must provide the buffer and initialize it
Example
size t EncodeStream (
In HANDLE hStream,
Inout STREAM *pstream) ; ](/Attachments/1-4f30bbaa60fc0e239be1482005f46c4c.png)
![Used to annotate a pointer to an array, which is both read and written by
the function
It is of size n elements, all of which must be valid in pre state
Example
void Foo (
Inout updates (1) Small Struct *pSS) ; ](/Attachments/1-a52f03ec974006039c8f90e66d0a564c.png)
![Return value
SAL 2
Ret notnull
_ Ret_maybenull_
_ Ret_writes_(size)
_ Ret_writes_bytes_(size)
_ Ret_writes_to_(size, count)
_ Ret_writes_bytes_to_(size, count)
Ret z
Return value is...
Not null
Might be null
Pointer to buffer of &#39;size&#39; valid
Pointer to buffer of &#39;size&#39; valid bytes
Pointer to buffer of &#39;size&#39; elements, first
&#39;count&#39; elements are valid
Pointer to buffer of &#39;size&#39; bytes, first
&#39;count&#39; bytes are valid
Pointer to null terminated string ](/Attachments/1-44f427c5fa920790895bedd65c68548d.png)
![SAL 2
_ Outptr_
_ Outptr_opt
_ Outptr_result_buffer_(size)
_ Outptr_result_bytebuffer_(size)
_ Outptr_result_maybenull_
_ Outptr_opt_result_maybenull_
Outref
Output pointers to buffer pointers and
out opt
Windows SAL 1
ere f
deref
d ere f
d ere f
_opt_out
deref_opt_out_opt
out_ecount(size)
out_bcount(size)* is equivalent for pointers to references ](/Attachments/1-73fb11d4a91c0bddb8ef07bbb7f7fd9e.png)
![_ Outptr_
Parameter is not null
Buffer is uninitialized
In the post state the result placed in the pointed-to location may not be
null, and must be valid.
Example
HRESULT CreateDescriptor (
outptr PSECURITY DESCRIPTOR *ppDescriptor) ](/Attachments/1-ffd50c3dc8de02a39318b1316e391a30.png)
![_ Outptr_result_buffer_(n)
Outptr_result_bytebuffer_(n)
Parameter is not null
In the post state the return pointer points to a buffer of size n elements/bytes
Example
void ElemCountExamp1e (
Outptr result buffer (n) wchar t * *buff ,
size t n)
*buff —
new char \[n*sizeof (wchar t) \] ; ](/Attachments/1-335f32d546f906cb9178ea3f873f2638.png)
![Parameter is not null
In the post state the return placed in the pointed-to location may be null.
Example
void Foo (
// pl is not null; *pl might be null
Outp tr
// both
Outptr
result maybenu11 int * *pl,
p2 and *p2 might be null
opt result maybenull int **p2) ; ](/Attachments/1-7d2d964b1f940edcb9621e35ef09c851.png)
![References
In Windows SAL 1, references are sometimes &quot;dereferenced&quot; like pointers
void GetDataBuffer (
deref out ecount (size)
int * &amp; pBuf,
deref out range (>=, MAX PATH)
out
In SAL 2 references are treated like references
void GetDataBuffer (
int&amp; size
int * &amp; pBuf,
Out ref result buffer (size)
int&amp; size
Out range , MAX PATH)
Out ](/Attachments/1-257895c945b502d491ecdd554838b41b.png)