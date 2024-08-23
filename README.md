This patch fixes a few problems and adds some minor improvements to Angana
Chakraborty's FOGSAA implementation. Download Chakraborty's implementation from
https://www.isical.ac.in/~bioinfo_miu/FOGSAA.7z

To use this patch, download the fogsaa-fixes.patch file to the source directory
of Chakraborty's implementation and run the following command in that
directory:
```
patch -lu fogsaa.cpp -i fogsaa-fixes.patch
```

Here is a list of the changes this patch makes:
- Adds warnings if the match score is negative or if the mismatch or gap scores
  are positive. These scores may cause issues with priority queue and lead to a
  buffer overflow. In some cases this buffer overflow can cause a segmentation
  fault.
- Adds NULL-pointer checks to the return values of fopen() and malloc() to
  prevent segmentation faults on permissions and out-of-memory errors.
- Fixes a heap underflow read during the alignment step. In most cases the
  heap underflow should not affect the program because the values read are not
  used, but if the buffer begins on a page boundary then accessing memory below
  the buffer may cause a segmentation fault if reading is disallowed on the
  page below.
- Silences warnings by some compilers by casting array indices to integers and
  commenting out an unused variable.
- Removes the "using namespace std;" statement, as using this namespace causes
  a name conflict with the "queue" type in the standard library and causes a
  compilation error on some compilers.
