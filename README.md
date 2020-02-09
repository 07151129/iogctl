iogctl
========

This is a patch to make the iogctl tool (IOGraphics control) build with the public SDK and open
source IOGraphics release.

Usage:

1. Extract IOGraphics source obtained from opensource.apple.com (tested with IOGraphics-530.60).
2. Apply the patch (`patch -p0 < IOGraphics.diff`).
3. Build iogctl (`xcodebuild -target iogctl`).
4. Add `iog=0x10000` to boot-args and reboot.
5. Run `iogctl -h` to see usage help.

iogctl is particularly useful for simulating clamshell events. For instance, invoking the following
commands

```
./iogctl injectCS.enable; ./iogctl injectCS.close
```

will simulate a clamshell close event, disabling the built-in display even if the lid is open. The
source of the program demonstrates the usage of IOGDiagnosticUserClient.

Warning: IOGDiagnosticUserClient does not check client process privilege, which may mean to denial
of service. Use at your own risk.
