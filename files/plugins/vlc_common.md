## vlc_fourcc_to_char {#vlc_fourcc_to_char}

```c
static inline void vlc_fourcc_to_char(vlc_fourcc_t fcc, char *psz_fourcc)
{
    memcpy(psz_fourcc, &fcc, 4);
}
```

### 函数描述
将 `vlc_fourcc_t` 类型的值转换为其字符串表示形式。该函数假设 `psz_fourcc` 中有足够的空间来存储 4 个字符。

### 函数参数说明

| 参数名     | 类型        | 描述                                                                 |
|------------|-------------|--------------------------------------------------------------------|
| `fcc`      | `vlc_fourcc_t` | 要转换的 `vlc_fourcc_t` 类型的值。                                   |
| `psz_fourcc` | `char *`      | 用于存储 `vlc_fourcc_t` 字符串表示形式的字符串指针。                |

### 函数返回值
该函数没有返回值。
## GCD {#GCD}

```c
static inline int64_t GCD(int64_t a, int64_t b)
{
    while(b)
    {
        int64_t c = a % b;
        a = b;
        b = c;
    }
    return a;
}
```

### 函数描述
`GCD` 函数用于计算两个 64 位整数 `a` 和 `b` 的最大公约数（Greatest Common Divisor, GCD）。该函数使用欧几里得算法（Euclidean algorithm）来计算最大公约数。

### 函数参数说明

| 参数名 | 类型     | 描述               |
| ------ | -------- | ------------------ |
| `a`    | `int64_t` | 第一个 64 位整数   |
| `b`    | `int64_t` | 第二个 64 位整数   |

### 函数返回值
- 返回值类型：`int64_t`
- 返回值说明：
  - 返回 `a` 和 `b` 的最大公约数。如果 `a` 和 `b` 都为 0，则返回 0。
## clip_uint8_vlc {#clip_uint8_vlc}

```c
static inline uint8_t clip_uint8_vlc( int32_t a )
{
    if( a&(~255) ) return (-a)>>31;
    else           return a;
}
```

### 函数描述
该函数用于将一个 32 位有符号整数 `a` 裁剪为 8 位无符号整数。如果 `a` 的值超出 8 位无符号整数的范围（即 0 到 255 之间），则返回 0 或 255，具体取决于 `a` 的符号。如果 `a` 在范围内，则直接返回 `a`。

### 函数参数说明

| 参数名 | 类型    | 描述                                                                 |
|--------|---------|--------------------------------------------------------------------------|
| `a`    | `int32_t` | 输入的 32 位有符号整数，需要被裁剪为 8 位无符号整数。 |

### 函数返回值
- 如果 `a` 的值在 0 到 255 之间，则返回 `a` 本身。
- 如果 `a` 的值小于 0，则返回 0。
- 如果 `a` 的值大于 255，则返回 255。
## clz {#clz}

```c
static inline unsigned clz(unsigned x)
```

### 描述
该函数用于计算无符号整数 `x` 的前导零的数量。前导零是指从最高有效位开始，连续的零的个数。

### 函数参数说明

| 参数 | 类型 | 描述 |
|------|------|------|
| `x`  | `unsigned` | 需要计算前导零的无符号整数 |

### 函数返回值
- 返回值为 `unsigned` 类型，表示 `x` 的前导零的数量。
- 如果 `x` 为 0，则返回值为 `sizeof(x) * 8`，即 `x` 的位数。
- 如果 `x` 不为 0，则返回值为从最高有效位开始，连续的零的个数。
## ctz {#ctz}

```c
static inline unsigned ctz (unsigned x)
{
#if VLC_GCC_VERSION(3,4)
    return __builtin_ctz (x);
#else
    unsigned i = sizeof (x) * 8;

    while (x)
    {
        x <<= 1;
        i--;
    }
    return i;
#endif
}
```

### 描述
该函数用于计算无符号整数 `x` 中末尾连续零的个数。如果 `x` 为零，则返回 `x` 的位宽（即 `sizeof(x) * 8`）。

### 参数说明
| 参数 | 类型 | 描述 |
|------|------|------|
| `x`  | `unsigned` | 要计算末尾零个数的无符号整数 |

### 返回值
- 如果 `x` 为零，返回 `sizeof(x) * 8`，即 `x` 的位宽。
- 否则，返回 `x` 中末尾连续零的个数。
## popcount {#popcount}

```c
static inline unsigned popcount(unsigned x)
```

### 描述
该函数用于计算无符号整数 `x` 中置位（即二进制表示中为1的位）的数量。它返回 `x` 中置位的数量。

### 函数参数说明

| 参数名 | 类型     | 描述               |
|--------|----------|--------------------|
| `x`    | `unsigned` | 需要计算置位数量的无符号整数 |

### 函数返回值
该函数返回 `x` 中置位的数量。返回值类型为 `unsigned`。
## parity {#parity}

```c
static inline unsigned parity (unsigned x)
{
#if VLC_GCC_VERSION(3,4)
    return __builtin_parity (x);
#else
    for (unsigned i = 4 * sizeof (x); i > 0; i /= 2)
        x ^= x >> i;
    return x & 1;
#endif
}
```

### 函数描述
`parity` 函数用于计算一个无符号整数的奇偶校验位。奇偶校验位是指一个二进制数中1的个数是奇数还是偶数。如果1的个数是奇数，则奇偶校验位为1；如果1的个数是偶数，则奇偶校验位为0。

### 函数参数说明

| 参数名 | 类型     | 描述               |
| ------ | -------- | ------------------ |
| `x`    | `unsigned` | 需要计算奇偶校验位的无符号整数 |

### 函数返回值
- 返回值类型：`unsigned`
- 返回值说明：
  - 如果输入的无符号整数 `x` 中1的个数是奇数，则返回 `1`。
  - 如果输入的无符号整数 `x` 中1的个数是偶数，则返回 `0`。
## bswap16 {#bswap16}

```c
static inline uint16_t bswap16(uint16_t x)
{
    return (x << 8) | (x >> 8);
}
```

### 函数描述
该函数用于交换16位整数的字节顺序。具体来说，它将输入的16位整数的字节顺序进行反转。

### 函数参数说明

| 参数名 | 类型    | 描述               |
|--------|---------|--------------------|
| `x`    | `uint16_t` | 需要进行字节交换的16位整数 |

### 函数返回值
函数返回交换字节顺序后的16位整数。
## bswap32 {#bswap32}

```c
static inline uint32_t bswap32(uint32_t x)
{
#if VLC_GCC_VERSION(4,3) || defined(__clang__)
    return __builtin_bswap32(x);
#else
    return ((x & 0x000000FF) << 24)
         | ((x & 0x0000FF00) <<  8)
         | ((x & 0x00FF0000) >>  8)
         | ((x & 0xFF000000) >> 24);
#endif
}
```

### 函数描述
`bswap32` 函数用于对32位整数进行字节交换（Byte swap）。它将输入的32位整数的字节顺序进行反转，即将最高有效字节（MSB）与最低有效字节（LSB）互换，次高有效字节与次低有效字节互换。

### 函数参数说明

| 参数名 | 类型     | 描述               |
|--------|----------|--------------------|
| `x`    | `uint32_t` | 需要进行字节交换的32位整数 |

### 函数返回值
函数返回经过字节交换后的32位整数值。具体来说，返回值是将输入的32位整数的字节顺序反转后的结果。
## bswap64 {#bswap64}

```c
static inline uint64_t bswap64 (uint64_t x)
{
#if VLC_GCC_VERSION(4,3) || defined(__clang__)
    return __builtin_bswap64 (x);
#elif !defined (__cplusplus)
    return ((x & 0x00000000000000FF) << 56)
         | ((x & 0x000000000000FF00) << 40)
         | ((x & 0x0000000000FF0000) << 24)
         | ((x & 0x00000000FF000000) <<  8)
         | ((x & 0x000000FF00000000) >>  8)
         | ((x & 0x0000FF0000000000) >> 24)
         | ((x & 0x00FF000000000000) >> 40)
         | ((x & 0xFF00000000000000) >> 56);
#else
    return ((x & 0x00000000000000FFULL) << 56)
         | ((x & 0x000000000000FF00ULL) << 40)
         | ((x & 0x0000000000FF0000ULL) << 24)
         | ((x & 0x00000000FF000000ULL) <<  8)
         | ((x & 0x000000FF00000000ULL) >>  8)
         | ((x & 0x0000FF0000000000ULL) >> 24)
         | ((x & 0x00FF000000000000ULL) >> 40)
         | ((x & 0xFF00000000000000ULL) >> 56);
#endif
}
```

### 函数描述
该函数用于对64位整数进行字节交换（Byte Swap）。字节交换是指将一个整数的字节顺序颠倒，例如将0x123456789ABCDEF0转换为0xF0DEBC9A78563412。

### 函数参数说明

| 参数名 | 类型     | 描述               |
|--------|----------|--------------------|
| `x`    | `uint64_t` | 需要进行字节交换的64位无符号整数。 |

### 函数返回值
- 返回值为经过字节交换后的64位无符号整数。
## U16_AT {#U16_AT}

```c
static inline uint16_t U16_AT (const void *p)
{
    uint16_t x;

    memcpy (&x, p, sizeof (x));
    return ntoh16 (x);
}
```

### 描述
该函数用于从指定内存地址 `p` 读取 16 位数据，并将其转换为网络字节序（大端序）。

### 函数参数说明

| 参数名 | 类型        | 描述                 |
|--------|-------------|----------------------|
| `p`    | `const void *` | 指向要读取的 16 位数据的内存地址。 |

### 函数返回值
- 返回值类型：`uint16_t`
- 返回值说明：返回从内存地址 `p` 读取的 16 位数据，并将其转换为网络字节序（大端序）。
## U32_AT {#U32_AT}

```c
static inline uint32_t U32_AT (const void *p)
{
    uint32_t x;

    memcpy (&x, p, sizeof (x));
    return ntoh32 (x);
}
```

### 描述
该函数用于从指定内存地址 `p` 读取 32 位数据，并将其转换为网络字节序（大端序）。

### 参数说明

| 参数名 | 类型       | 描述                   |
|--------|------------|------------------------|
| `p`    | `const void *` | 指向要读取的 32 位数据的内存地址。 |

### 返回值
函数返回从内存地址 `p` 读取的 32 位数据，并将其转换为网络字节序（大端序）后的值。
## U64_AT {#U64_AT}

```c
static inline uint64_t U64_AT(const void *p)
{
    uint64_t x;
    memcpy(&x, p, sizeof(x));
    return ntoh64(x);
}
```

### 描述
该函数用于从指定内存地址 `p` 读取 64 位数据，并将其转换为网络字节序（大端序）。

### 参数说明

| 参数名 | 类型        | 描述                         |
|--------|-------------|------------------------------|
| `p`    | `const void *` | 指向要读取的 64 位数据的内存地址。 |

### 返回值
函数返回从内存地址 `p` 读取的 64 位数据，并将其转换为网络字节序（大端序）后的值。
## GetWLE {#GetWLE}

```c
static inline uint16_t GetWLE(const void *p)
```

### 描述
该函数用于以小端序（little-endian）读取16位数据。

### 函数参数说明

| 参数名 | 类型 | 描述 |
|--------|------|------|
| `p`    | `const void *` | 指向要读取的16位数据的指针。 |

### 函数返回值
函数返回从指针 `p` 读取的16位数据，以小端序表示。如果系统是大端序（big-endian），则函数内部会自动进行字节序转换。
## GetDWLE {#GetDWLE}

```c
static inline uint32_t GetDWLE(const void *p)
```

### 描述
该函数用于以小端序（little-endian）读取32位数据。

### 函数参数说明

| 参数名 | 类型        | 描述                   |
|--------|-------------|------------------------|
| `p`    | `const void *` | 指向要读取的32位数据的指针 |

### 函数返回值
- 返回值类型：`uint32_t`
- 返回值说明：返回从指针 `p` 读取的32位数据，以小端序表示。如果系统是大端序（big-endian），则返回值会自动转换为小端序。
## GetQWLE {#GetQWLE}

```c
static inline uint64_t GetQWLE(const void *p)
```

### 函数描述
该函数用于以小端序（little-endian）读取64位数据。

### 函数参数说明

| 参数名 | 类型        | 描述                 |
|--------|-------------|----------------------|
| `p`    | `const void *` | 指向要读取的64位数据的指针 |

### 函数返回值
函数返回从指针 `p` 读取的64位数据，以小端序表示。如果系统是大端序（big-endian），则返回值会经过字节交换处理。
## SetWBE {#SetWBE}

```c
static inline void SetWBE(void *p, uint16_t w)
{
    w = hton16(w);
    memcpy(p, &w, sizeof(w));
}
```

### 函数描述
该函数用于将一个16位的整数转换为网络字节序（大端序），并将其写入指定的内存位置。

### 函数参数说明

| 参数名 | 类型     | 描述                                       |
|--------|----------|--------------------------------------------|
| `p`    | `void*`  | 指向目标内存位置的指针，用于存储转换后的16位整数。 |
| `w`    | `uint16_t` | 需要转换为网络字节序的16位整数。            |

### 函数返回值
该函数没有返回值（`void`）。
## SetDWBE {#SetDWBE}

```c
static inline void SetDWBE(void *p, uint32_t dw)
{
    dw = hton32(dw);
    memcpy(p, &dw, sizeof(dw));
}
```

### 函数描述
该函数用于将32位整数以网络字节序（大端序）写入指定的内存位置。

### 函数参数说明

| 参数名 | 类型     | 描述                                                                 |
|--------|----------|--------------------------------------------------------------------------|
| `p`    | `void*`  | 指向目标内存位置的指针，该位置将存储转换后的32位整数。 |
| `dw`   | `uint32_t` | 要写入的32位整数值，在写入前会被转换为网络字节序。 |

### 函数返回值
该函数没有返回值（`void`）。
## SetQWBE {#SetQWBE}

```c
static inline void SetQWBE(void *p, uint64_t qw)
{
    qw = hton64(qw);
    memcpy(p, &qw, sizeof(qw));
}
```

### 函数描述
该函数用于将64位整数以网络字节序（大端序）写入指定的内存位置。

### 函数参数说明

| 参数名 | 类型      | 描述                                                                 |
|--------|-----------|----------------------------------------------------------------------|
| `p`    | `void *`  | 指向目标内存位置的指针，函数将64位整数写入该位置。                   |
| `qw`   | `uint64_t`| 要写入的64位整数值，函数会将其转换为网络字节序（大端序）后写入内存。|

### 函数返回值
该函数没有返回值（`void`）。
## SetWLE {#SetWLE}

```c
static inline void SetWLE(void *p, uint16_t w)
{
#ifdef WORDS_BIGENDIAN
    w = bswap16(w);
#endif
    memcpy(p, &w, sizeof(w));
}
```

### 函数描述
该函数用于以小端序（Little Endian）格式写入16位数据。如果系统是大端序（Big Endian），则会在写入前将数据转换为小端序格式。

### 函数参数说明

| 参数名 | 类型      | 描述                                                                 |
| ------ | --------- | -------------------------------------------------------------------- |
| `p`    | `void *`  | 指向目标内存地址的指针，用于写入16位数据。                           |
| `w`    | `uint16_t`| 要写入的16位数据值。                                                 |

### 函数返回值
该函数没有返回值（`void`）。
## SetDWLE {#SetDWLE}

```c
static inline void SetDWLE(void *p, uint32_t dw)
{
#ifdef WORDS_BIGENDIAN
    dw = bswap32(dw);
#endif
    memcpy(p, &dw, sizeof(dw));
}
```

### 函数描述
该函数用于以小端序（little endian）格式写入32位数据。如果系统是大端序（big endian），则会在写入前将数据转换为小端序格式。

### 函数参数说明

| 参数名 | 类型      | 描述                     |
|--------|-----------|--------------------------|
| `p`    | `void *`  | 指向目标内存地址的指针   |
| `dw`   | `uint32_t`| 要写入的32位无符号整数   |

### 函数返回值
该函数没有返回值（`void`）。
## SetQWLE {#SetQWLE}

```c
static inline void SetQWLE(void *p, uint64_t qw)
```

### 函数描述
该函数用于以小端序（Little Endian）格式写入64位数据。如果系统是大端序（Big Endian），则会在写入前将数据转换为小端序格式。

### 函数参数说明

| 参数名 | 类型      | 描述                                                         |
| ------ | --------- | ------------------------------------------------------------ |
| `p`    | `void *`  | 指向目标内存地址的指针，用于存储64位数据。                   |
| `qw`   | `uint64_t`| 要写入的64位数据。                                           |

### 函数返回值
该函数没有返回值（`void`）。
## vlc_ureduce {#vlc_ureduce}

```c
VLC_API bool vlc_ureduce( unsigned *pi_dst_num, unsigned *pi_dst_den, uint64_t i_src_num, uint64_t i_src_den, uint64_t i_max);
```

### 函数描述

该函数用于将分数 `i_src_num / i_src_den` 约简为最简分数，并将结果存储在 `pi_dst_num` 和 `pi_dst_den` 中。如果约简后的分母超过 `i_max`，则函数返回 `false`，否则返回 `true`。

### 函数参数说明

| 参数名        | 类型      | 描述                                                                 |
|---------------|-----------|----------------------------------------------------------------------|
| `pi_dst_num`  | `unsigned*` | 指向存储约简后分子结果的指针。                                       |
| `pi_dst_den`  | `unsigned*` | 指向存储约简后分母结果的指针。                                       |
| `i_src_num`   | `uint64_t` | 原始分数的分子。                                                     |
| `i_src_den`   | `uint64_t` | 原始分数的分母。                                                     |
| `i_max`       | `uint64_t` | 允许的最大分母值。如果约简后的分母超过此值，函数将返回 `false`。     |

### 函数返回值

- **`true`**: 如果分数成功约简并且约简后的分母不超过 `i_max`。
- **`false`**: 如果约简后的分母超过 `i_max`。
## vlc_free {#vlc_free}

```c
static void vlc_free(void *ptr)
{
    if (ptr)
        free((char*)ptr - ((char*)ptr)[-1]);
}
```

### 描述
`vlc_free` 函数用于释放通过 `vlc_alloc` 分配的内存。它首先检查指针是否为空，如果不为空，则调用 `free` 函数释放内存。

### 函数参数说明

| 参数名 | 类型 | 描述 |
| ------ | ---- | ---- |
| `ptr`  | `void*` | 指向要释放的内存块的指针。如果为 `NULL`，则函数不执行任何操作。 |

### 函数返回值
该函数没有返回值。
## abort 

```c
void abort(void);
```

### 描述
`abort` 函数用于立即终止当前进程的执行。它会向调用进程发送一个未处理的 `SIGABRT` 信号，通常会导致进程终止并生成核心转储文件。此函数不会返回，调用它的进程将被终止。

### 函数参数说明
此函数没有参数。

| 参数名 | 类型 | 描述 |
|--------|------|------|
| 无     | 无   | 无   |

### 函数返回值
`abort` 函数不会返回任何值，因为它会导致进程终止。
## abort 

```c
void abort(void);
```

### 描述
`abort` 函数用于立即终止程序的执行。它会导致程序异常终止，通常会生成一个核心转储文件（如果系统支持），并且不会进行正常的程序终止清理操作，如调用 `atexit` 注册的函数。

### 参数说明
此函数没有参数。

| 参数名 | 类型 | 描述 |
|--------|------|------|
| 无     | 无   | 无   |

### 返回值
`abort` 函数不会返回，因为它会导致程序立即终止。
## abort 

```c
void abort(void);
```

### 描述
`abort` 函数用于立即终止程序的执行。它不会正常地终止程序，而是通过发送一个未处理的信号（通常是 `SIGABRT`）来强制终止程序。调用 `abort` 函数通常用于在程序遇到无法恢复的错误时强制退出。

### 函数参数说明
| 参数名 | 类型 | 描述 |
|--------|------|------|
| 无     | 无   | 无   |

### 函数返回值
`abort` 函数不会返回，因为它会导致程序的终止。调用 `abort` 后，程序将立即终止，不会返回到调用点。
## abort 

```c
void abort(void);
```

### 描述
`abort` 函数用于立即终止程序的执行。它不会正常地清理资源或执行任何其他清理操作。调用 `abort` 函数通常会导致程序异常终止，并生成一个核心转储文件（如果系统配置允许）。

### 函数参数说明

| 参数名 | 类型 | 描述 |
|--------|------|------|
| 无     | 无   | 无   |

### 函数返回值
`abort` 函数不会返回任何值，因为它会导致程序立即终止。
## vlc_list_t {#vlc_list_t}

```c
struct vlc_list_t
{
    int             i_count;
    vlc_value_t *   p_values;
    int *           pi_types;
};
```

### 描述
`vlc_list_t` 结构体用于表示一个 VLC 列表。该结构体包含列表中元素的数量、元素的值以及元素的类型。

### 结构体成员说明

| 成员变量 | 类型          | 描述                                                                 |
|----------|---------------|--------------------------------------------------------------------------|
| `i_count`| `int`         | 列表中元素的数量。                                                     |
| `p_values`| `vlc_value_t *`| 指向列表中元素值的指针。每个元素的值由 `vlc_value_t` 类型表示。       |
| `pi_types`| `int *`       | 指向列表中元素类型的指针。每个元素的类型由一个整数表示。               |

### 返回值
该结构体本身没有返回值，因为它是一个定义，用于描述数据结构。
