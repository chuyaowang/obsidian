# openssl

## bug

Multiple versions installed

homebrew ver
/opt/homebrew/Cellar/openssl@3/3.3.1/lib

miniconda ver
/opt/homebrew/Caskroom/miniconda/base/pkgs/openssl-3.2.1-h0d3ecfb_0/lib

Encounter error when installing openssl package:

Error: package or namespace load failed for ‘openssl’ in dyn.load(file, DLLpath = DLLpath, ...):
 unable to load shared object '/Users/wangchuyao/R Projects/grnAnalysis/renv/library/R-4.2/x86_64-apple-darwin17.0/00LOCK-openssl/00new/openssl/libs/openssl.so':
  dlopen(/Users/wangchuyao/R Projects/grnAnalysis/renv/library/R-4.2/x86_64-apple-darwin17.0/00LOCK-openssl/00new/openssl/libs/openssl.so, 0x0006): tried: '/Users/wangchuyao/R Projects/grnAnalysis/renv/library/R-4.2/x86_64-apple-darwin17.0/00LOCK-openssl/00new/openssl/libs/openssl.so' (mach-o file, but is an incompatible architecture (have 'arm64', need 'x86_64')), '/System/Volumes/Preboot/Cryptexes/OS/Users/wangchuyao/R Projects/grnAnalysis/renv/library/R-4.2/x86_64-apple-darwin17.0/00LOCK-openssl/00new/openssl/libs/openssl.so' (no such file), '/Users/wangchuyao/R Projects/grnAnalysis/renv/library/R-4.2/x86_64-apple-darwin17.0/00LOCK-openssl/00new/openssl/libs/openssl.so' (mach-o file, but is an incompatible architecture (have 'arm64', need 'x86_64'))

**Cause**: complier complies for arm64, but my r is x86. Can's solve without breaking the other renv environment.