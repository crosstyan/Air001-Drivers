# Air001 Drivers HAL and LL

customized for [crosstyan/air001-cmake-hal](https://github.com/crosstyan/air001-cmake-hal).

Looks like [air001](https://wiki.luatos.org/chips/air001/index.html)
is the same chip as [py32f0](https://github.com/decaday/PY32_Docs).

I should look into it later.

## CMake

See [air001-cmake-hal](https://github.com/crosstyan/air001-cmake-hal/blob/81c16517ab7fa3471b26f6c1416741c8f0bacd9c/lib/CMakeLists.txt#L1-L25)

## DSP

Upstream is [ARM-software/CMSIS-DSP](https://github.com/ARM-software/CMSIS-DSP).
Seems an old version of CMSIS-DSP is included,
but I can't really see if it's used anywhere in Arduino.

## See Also

- [decaday/py32f0_cmake_template](https://github.com/decaday/py32f0_cmake_template)
- [decaday/PY32F0_Drivers](https://github.com/decaday/PY32F0_Drivers)
- [Air-duino/Air001-Drivers](https://github.com/Air-duino/Air001-Drivers) (upstream)
