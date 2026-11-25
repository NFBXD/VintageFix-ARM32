# VintageFix ARM32 Fix

> **Unofficial fork** of [embeddedt/VintageFix](https://github.com/embeddedt/VintageFix) 0.7.2. Licensed under the same GNU Lesser General Public License (LGPL) as the original.

This fork fixes a JVM crash on 32-bit ARM devices (SIGBUS / BUS_ADRALN in libjvm.so, thread "JarDiscovererCache save thread").

## What changed
Kryo's `UnsafeInput` / `UnsafeOutput` write values to unaligned memory addresses, which 32-bit ARM does not allow. In these two files they were replaced with the regular `Input` / `Output`:

- `src/main/java/org/embeddedt/vintagefix/jarcache/JarDiscovererCache.java`
- `src/main/java/org/embeddedt/vintagefix/transformercache/TransformerCache.java`

No other code was changed.

## Notes
- The cache format differs from the original. Delete `jarDiscovererCache.dat` and `transformerCache.dat` before the first launch.
- Do not use this jar together with the original VintageFix (same mod ID).
- Tested on: POCO C61, Android 16, FCL, OpenJDK 8 (aarch32), Minecraft 1.12.2, Forge 14.23.5.2864.
- If you do not use a 32-bit ARM device, use the original mod instead.

The rest of this README is the original project's.

---

# VintageFix

Experimental performance mod for 1.12, intended to expand upon and replace FoamFix.

Requires MixinBooter.

Includes a small portion of Fabric API code, used under terms of Apache-2.0.

Download: https://nightly.link/embeddedt/VintageFix/workflows/gradle/main/Package.zip

Discord: https://discord.gg/rN9Y7caguP (#vintagefix-discussion channel)
