# git-experiments

Assumes the remote is called `package`. 

For example: 

```bash=
git remote add package git@github.com:buckaroo-pm/mapbox-rapidjson.git
```

## Fetching the Branches

```bash=
$ time git ls-remote --heads package 
5b6e40df26db79a33cd1974bcdeb6a433c49c003	refs/heads/cmake_CMP0054
d7ee08621a364693cdc610a98fb5bf556efef084	refs/heads/coverage
00ed0a5f91618257f4700b575af2e10247f19e67	refs/heads/example
c62a19cfbdbc5f49c5933226db91de5844590f6a	refs/heads/example_parsebyparts
f7eb184446c3e59fb7df4441ca624d967b73d1e8	refs/heads/gh-pages
3595b1f677a2cc331dfea301cccf06cca0caa5d1	refs/heads/issue158_parsestdstring
e7cb2b1cbf5220b614c62d8a3ce1fa45965f1ffe	refs/heads/issue205
9f6736c2ccbf74c5fa4a0fad915f086dd3a7b5b5	refs/heads/issue316_templatedaccessors
964d89e34bb0b8dd3231dd9805d6b6b87bfe6b0d	refs/heads/issue325
98ddfacdf1f4fc8281190999c801d8872c08a06e	refs/heads/issue341_float
1d856b2761ced15984360e60ad3b372b67d6e5cd	refs/heads/issue362
60116cf11ef635e0ed0e3d4aba2724cbdc65a567	refs/heads/issue538_regexzeromin
7a9166f3628b29341d9f280113847ad698b60ad7	refs/heads/issue552_movingschemadocument
fa8c676b37056d83992119e4ebdc6954befff3e8	refs/heads/issue583_regexcrash
bbcdb8b574b4098f95d95efda046705a39f888c9	refs/heads/issue608_required
332b61fe412f43dc4b81f8cc084b1d21f1b73c93	refs/heads/issue682_mallocfail
db6a6f3f64897eb009f8635535f1bc6212265825	refs/heads/issue684_flush
0f9dbe0a9c78b6a8163e47a4b5e1c5df7a3360b9	refs/heads/issue716_parsebyparts
44ccecfb229c4862ef4fa924a4841749196abfc7	refs/heads/master
b8c83c53b113f297d9eb56bf0ce4f29a6532a6dc	refs/heads/optimization
ce3ca58fee67c1b2e90bcb742bc8d7f1dc87ac34	refs/heads/pr/651
f191cd9dfcf58efd10439e65c7c14d5fbaa5ff38	refs/heads/regex
16872af88915176f49e389defb167f899e2c230a	refs/heads/silence-dereference-null-pointer
facb432f91b588b282c42d2a1a643894ae550e8f	refs/heads/travis
12425693ba255b8b8d68ba8ce752a23a25c2118f	refs/heads/vcwarning
2fb78f9cee01996f020d5af7592b37c5a0693b31	refs/heads/version1.1.0
cb927a24ca5f7b0794f049369a427012d5df8695	refs/heads/zh-doc

real	0m1.511s
user	0m0.028s
sys	0m0.020s
```

## Fetching the Commits

```bash=
$ time git fetch --all

real	0m1.471s
user	0m0.047s
sys	0m0.038s
```

This is much slower on the first run! 

```bash=
$ time git log package/master --pretty=format:"%h" > commits.txt

real	0m0.033s
user	0m0.023s
sys	0m0.007s
```

## Fetching Manifest

To fetch the remote tree of files (might be useful): 

```bash=
$ time git ls-tree -r package/master --name-only
.buckconfig
.gitattributes
.gitignore
.gitmodules
.travis.yml
BUCK
CHANGELOG.md
CMakeLists.txt
...
bin/types/readme.txt
buckaroo.toml
doc/CMakeLists.txt
doc/Doxyfile.in
...
test/unittest/valuetest.cpp
test/unittest/writertest.cpp
thirdparty/gtest
travis-doxygen.sh

real	0m0.044s
user	0m0.007s
sys	0m0.010s
```

To fetch one file: 

```bash=
$ time git show remotes/package/master:buckaroo.toml
targets = [ "//:rapidjson" ]

real	0m0.023s
user	0m0.009s
sys	0m0.012s
```

Or for a particular commit: 

```bash=
$ time git show 44ccecfb229c4862ef4fa924a4841749196abfc7:buckaroo.toml
targets = [ "//:rapidjson" ]

real	0m0.125s
user	0m0.011s
sys	0m0.037s
```

However, you must `git fetch` first! 
