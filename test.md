**Featured updates:**


- crypto publicEncrypt and privateDecrypt added 

- Shared Memory Store, Buffer Type Support GH [#716](https://github.com/jxcore/jxcore/issues/716) 

- ECDH ported from 0.12.x GH [#619](https://github.com/jxcore/jxcore/issues/619) 

- Multiple engine version support 
    This update brings v8 3.28 support to comply with Chakra shim on Win
    RT.

- packaging format changed to binary GH [#508](https://github.com/jxcore/jxcore/issues/508) 

- Windows UWP support 

- Windows IOT and Mobile support 


**Issues:**


- SM: Error tooling compatibility updates GH [#728](https://github.com/jxcore/jxcore/issues/728) 
    With this commit, SM Error tooling should be fairly compatible with v8

- [SM] stack[0].getFileName() missing GH [#728](https://github.com/jxcore/jxcore/issues/728) 

- deprecate jx-ni JX_Initialize GH [#723](https://github.com/jxcore/jxcore/issues/723) 

- SM: ghost cannot start due to sqlite error GH [#540](https://github.com/jxcore/jxcore/issues/540) 

- Segfault (asm.js + spidermonkey) GH [#624](https://github.com/jxcore/jxcore/issues/624) 

- HTTP IncomingMessage constructor not recognized GH [#681](https://github.com/jxcore/jxcore/issues/681) 

- subthreads waiting for package to load. Fixes GH [#709](https://github.com/jxcore/jxcore/issues/709) 

- Remove max compression ratio limit GH [#703](https://github.com/jxcore/jxcore/issues/703) 

- allow --prefix to be both relative and absolute. Applies to GH [#657](https://github.com/jxcore/jxcore/issues/657). Closes GH [#675](https://github.com/jxcore/jxcore/issues/675) 

- async readFile catches sync exception. Closes GH [#634](https://github.com/jxcore/jxcore/issues/634) 

- Fix when stdout and stderr don't use file descriptors 1 & 2, issue GH [#608](https://github.com/jxcore/jxcore/issues/608). 
    Detect when running in an environment that doesn't use file descriptors 1 & 2 for stdout and stderr streams, such as Windows GUI applications. Using those descriptors will throw an exception at engine startup, which would prevent the source file given to JX_DefineMainFile from running.

- More detailed stack traces from threads GH [#655](https://github.com/jxcore/jxcore/issues/655) 

- use ./ rather than / for DESTDIR. Closes GH [#657](https://github.com/jxcore/jxcore/issues/657) 

- SM: fixes unicode issue GH [#641](https://github.com/jxcore/jxcore/issues/641) 
    Reduces the number of memory allocation requests

- android warning for global modules installation as root. Applies to GH [#628](https://github.com/jxcore/jxcore/issues/628) 

- ~/.jx and ~/.npm proper ownership with `sudo jx install`. Closes GH [#645](https://github.com/jxcore/jxcore/issues/645) 

- fix finding jx.config / node.config on Windows. Closes GH [#642](https://github.com/jxcore/jxcore/issues/642) 

- fix for jx --debug GH [#623](https://github.com/jxcore/jxcore/issues/623) 

- _cmp() accept buffer GH [#508](https://github.com/jxcore/jxcore/issues/508) 

- fix test-chdir for el-capitan GH [#641](https://github.com/jxcore/jxcore/issues/641) 
    credit goes to @silverwind
    https://github.com/nodejs/node/commit/ddf258376dd35d5813255b921701a75b28
    611979

- Efficiently repair reading of signed files GH [#583](https://github.com/jxcore/jxcore/issues/583) 
    Uses a new method for finding the data to load; Fixes an issue with
    signing a Windows executable

- test: handle error message from new V8 engine in test-domain.js (ref: GH [#585](https://github.com/jxcore/jxcore/issues/585)) 

- src: fix possible crash in node_crypto.cc:EIO_PBKDF2After() variants (GH [#585](https://github.com/jxcore/jxcore/issues/585)) 

- src: fix TCPWrap::InstantiateCOM() in case of NULL argument (ref: GH [#585](https://github.com/jxcore/jxcore/issues/585)) 

- command line --sign support restored. Applies to GH [#583](https://github.com/jxcore/jxcore/issues/583) 

- net-tcp test much improved. Applies to GH [#205](https://github.com/jxcore/jxcore/issues/205) 

- stream._writev method added GH [#571](https://github.com/jxcore/jxcore/issues/571) 

- jxm java client doc update on object reading. closes jxcore/jxmGH [#29](https://github.com/jxcore/jxcore/issues/29) 

- reset event added to repl GH [#571](https://github.com/jxcore/jxcore/issues/571) 

- lookup event added to net GH [#571](https://github.com/jxcore/jxcore/issues/571) 

- path.isAbsolute method added GH [#571](https://github.com/jxcore/jxcore/issues/571) 

- setDefaultEncoding method added to writable stream GH [#571](https://github.com/jxcore/jxcore/issues/571) 

- cork and uncork methods added in writable stream GH [#571](https://github.com/jxcore/jxcore/issues/571) 


**Other:**


- uv: assert for a wrongly initialized instance 

- v8: use isolate from commons 

- module: minor perf. update 
    - proxy debug output to console.error
    - do not pre-compile(JSON.stringify) the arguments

- remove customLogInterface from console 
    This was pre mobile-support implementation and no longer needed

- jx-ni: add JXEngine reference for internal sub instances 

- jx-ni: New Method - JX_SetNativeMethod 

- give exec right to jx-ni run-tests script 

- jx-ni: fix GetGlobal and GetProcess scoping 
    After this fix, both methods are callable without being inside a
    function call.

- fix leaking nanosecond issue on Posix 

- omit space in version string 

- define CC and CCX explicitly from node 4.x 

- v8-328: Use prime type index for indexedProperties 

- jx-ni: add assert message (initialize after shutdown) 

- Add Android ARM64 compilation option 

- SM build no longer needs `which` installation 

- uv-unix: implement proxy uv_run for ABI compatibility 

- log: do not force assert 

- Windows: log to temp folder if no std or debugger available 

- SM: prevent VS2015 resolving wrong include path 

- Prevent crash WinIOT failing to get processor name 
    double check the result for GetLastError

- winonecore: interface compatibility for logging 

- Chakra: Enable debugger [initial] 

- SM: force static JS API [for method signatures on Windows] 

- SM: win-onecore use trampoline-none 

- SM: do not force char16_t redefinition for VS2015+ [fix condition] 

- force include windows.h for debugger logging 

- add leveldown-mobile to win-onecore builds 

- ECDH ported from 0.12.x 

- Update test_rsa_privkey_encrypted.pem 

- v8-328: Debugger support 

- use char pointer for memory store 

- travis: do not force jslint on travis 

- utf_man: use const for constant variable 

- SM: VS2015+ do not force char16_t 

- update leveldown-mobile for UWP support 

- jx install: support spaces in HOME_PATH 

- v8.314: TO_LOCAL_ARRAY Persistent + V8Object together 
    Previous implementations support either Persistent or Object etc.
    (Local, Handle) types.

- open-wrt: simplify apt-get install 

- open-wrt: use exec() instead of cmdSync() for git clone 

- v8: fix isolate deadlock 

- Windows: share path conf. with WinRT 

- WinRT: module boost resolve 

- WinRT: fs basic simulate realpathSync 

- WinRT: redirect core.console to debug window 

- use bigger log buffer 

- combine console loggers & make UWP logging available globally 

- llvm-format on util files 

- UWP support final 

- WinRT: do not include ole32 

- WinRT:  do not use default libs 

- WinRT: log to debug Window (all jxcore logs) 

- no pipe-creation for WinRT 

- openssl-no-asm by default for WinRT 

- disable UnregisterWait for WinRT 

- log to debug window for WinRT 

- sqlite winrt 

- WinOneCore: Do not use RegisterWaitForSingleObject 

- disable spawn for win one core 

- sqlite is updated to 3.9.1.0 

- win-onecore command line switch 

- handle zero-length Buffer(0) 
    It is a perfectly valid scenario in both Javascript and C/C++ to have a
    buffer of zero length, so we must handle this. (strlen(nullptr) would
    crash)

- update memory-leak for v8 3.2+ 

- v8-3+ compatibility : do not use persistent argument 

- jxcore now has built-in uwp interface 

- uv-pipe: prevent assert crash for winonecore not supported 

- replace NAN to JX macro 

- Run simple test suite on both engines in Travis CI 
    Skip a couple of troublesome tests in Travis CI
    NOTE: A shell trick is used here since Travis CI only seems to check the result
    of the last command in the script: section.

- added JX_GetBuffer() to native interface for accessing Buffers directly 

- jxcore runs on WindowsARM 

- vcbuild: WinARM doesn't support openssl-asm 

- uv: force define __arm__ for WinARM 

- uv: winthreads pthread force cancel sync form ARM 

- vcbuild:Windows one-core option 

- lib: cleanup trailing whitespace in lib/jx/_jx_incoming.js 

- lib: fix jslint errors (also exclude lib/jx/_jx_marker.js from jslint again) 

- openssl win10 SDK fix 

- don't force define timespec for VS2015+ 

- openssl win-arm 

- Added arch build scripts 

- jxcore tests: assert in thread does not cause thread restarting 

- V8:fix envQuery 

- do not double persistent to local 


