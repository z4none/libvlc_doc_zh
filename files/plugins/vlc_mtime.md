## mstrtime {#mstrtime}

```c
VLC_API char * mstrtime( char *psz_buffer, mtime_t date );
```

### 描述
该函数用于将 `mtime_t` 类型的时间值转换为可读的字符串格式，并将结果存储在提供的缓冲区中。

### 函数参数说明

| 参数名       | 类型      | 描述                                                                 |
|--------------|-----------|--------------------------------------------------------------------------|
| psz_buffer   | char *    | 指向存储结果字符串的缓冲区的指针。缓冲区的大小应至少为 `MSTRTIME_MAX_SIZE`。 |
| date         | mtime_t   | 要转换的时间值，通常是以微秒为单位的时间戳。                             |

### 函数返回值
- 成功时，返回指向 `psz_buffer` 的指针，即转换后的字符串。
- 如果 `psz_buffer` 为 `NULL`，则返回 `NULL`。
## secstotimestr {#secstotimestr}

```c
VLC_API char * secstotimestr( char *psz_buffer, int32_t secs );
```

### 描述
该函数将给定的秒数转换为时间字符串，并将结果存储在提供的缓冲区中。时间字符串的格式为 `HH:MM:SS`，其中 `HH` 表示小时，`MM` 表示分钟，`SS` 表示秒。

### 函数参数说明

| 参数名       | 类型      | 描述                                                                 |
|--------------|-----------|----------------------------------------------------------------------|
| `psz_buffer` | `char *`  | 指向缓冲区的指针，用于存储转换后的时间字符串。缓冲区的大小应至少为 9 字节（包括终止符 `\0`）。 |
| `secs`       | `int32_t` | 要转换的秒数。                                                       |

### 函数返回值
- 返回值为 `psz_buffer`，即指向转换后的时间字符串的指针。
- 如果 `secs` 为负数，则返回的时间字符串为 `"--:--"`。
- 如果 `psz_buffer` 为 `NULL`，则函数返回 `NULL`。
## date_Init {#date_Init}

```c
VLC_API void date_Init( date_t *p_date, uint32_t i_divider_n, uint32_t i_divider_d );
```

### 描述
该函数用于初始化一个 `date_t` 结构体。它设置了日期结构体的分母和分子，以便后续使用。

### 函数参数说明

| 参数名        | 类型      | 描述                                                         |
|---------------|-----------|--------------------------------------------------------------|
| `p_date`      | `date_t *`| 指向要初始化的 `date_t` 结构体的指针。                       |
| `i_divider_n` | `uint32_t`| 分母的分子部分，用于计算日期的时间戳。                       |
| `i_divider_d` | `uint32_t`| 分母的分母部分，用于计算日期的时间戳。                       |

### 函数返回值
该函数没有返回值。
## date_Change {#date_Change}

```c
VLC_API void date_Change( date_t *p_date, uint32_t i_divider_n, uint32_t i_divider_d );
```

### 描述
该函数用于更改 `date_t` 结构的分频器。分频器用于将输入的采样率转换为输出采样率。

### 函数参数说明

| 参数名        | 类型      | 描述                                                                 |
|---------------|-----------|--------------------------------------------------------------------------|
| `p_date`      | `date_t *` | 指向 `date_t` 结构的指针，该结构用于存储日期和时间信息。                |
| `i_divider_n` | `uint32_t` | 分频器的分子部分，表示输入采样率与输出采样率之间的比率的分子。         |
| `i_divider_d` | `uint32_t` | 分频器的分母部分，表示输入采样率与输出采样率之间的比率的分母。         |

### 函数返回值
该函数没有返回值。
## date_Set {#date_Set}

```c
VLC_API void date_Set( date_t *p_date, mtime_t i_pts );
```

### 描述
该函数用于设置 `date_t` 结构体的时间戳。它将给定的 `mtime_t` 类型的时间戳 `i_pts` 赋值给 `date_t` 结构体 `p_date`。

### 函数参数说明

| 参数名 | 类型 | 描述 |
| --- | --- | --- |
| `p_date` | `date_t *` | 指向 `date_t` 结构体的指针，用于存储设置的时间戳。 |
| `i_pts` | `mtime_t` | 要设置的时间戳值，通常表示为微秒。 |

### 函数返回值
该函数没有返回值。
## date_Get {#date_Get}

```c
VLC_API mtime_t date_Get(const date_t *date);
```

### 描述
该函数用于获取日期对象的当前时间值。

### 函数参数说明

| 参数名 | 类型       | 描述               |
|--------|------------|--------------------|
| date   | const date_t* | 指向日期对象的指针 |

### 函数返回值
该函数返回日期对象的当前时间值，类型为 `mtime_t`。
## date_Move {#date_Move}

```c
VLC_API void date_Move( date_t *p_date, mtime_t i_delay );
```

### 函数描述
该函数用于将日期对象 `p_date` 向前或向后移动指定的 `i_delay` 时间。`i_delay` 是一个以微秒为单位的时间值。

### 函数参数说明

| 参数名   | 类型    | 描述                                                         |
|----------|---------|--------------------------------------------------------------|
| `p_date` | `date_t*` | 指向日期对象的指针，该对象的时间将被调整。                   |
| `i_delay`| `mtime_t` | 以微秒为单位的时间值，表示日期对象需要移动的时间量。正值表示向前移动，负值表示向后移动。 |

### 函数返回值
该函数没有返回值。
## date_Increment {#date_Increment}

```c
VLC_API mtime_t date_Increment( date_t *p_date, uint32_t i_nb_samples );
```

### 描述
该函数用于增加 `date_t` 结构体中的时间值。它根据给定的样本数 `i_nb_samples` 来更新 `p_date` 指向的 `date_t` 结构体中的时间。

### 函数参数说明

| 参数名        | 类型      | 描述                                                         |
|---------------|-----------|--------------------------------------------------------------|
| `p_date`      | `date_t*` | 指向 `date_t` 结构体的指针，表示要更新的时间。               |
| `i_nb_samples`| `uint32_t`| 要增加的样本数，用于计算新的时间值。                         |

### 函数返回值
该函数返回更新后的时间值，类型为 `mtime_t`。返回值表示更新后的时间，单位为微秒（µs）。
## date_Decrement {#date_Decrement}

```c
VLC_API mtime_t date_Decrement( date_t *p_date, uint32_t i_nb_samples );
```

### 描述

该函数用于减少 `date_t` 结构体中的时间值。它将 `p_date` 指向的日期减少 `i_nb_samples` 个样本的时间长度，并返回减少后的时间值。

### 函数参数说明

| 参数名        | 类型      | 描述                                                                 |
|---------------|-----------|--------------------------------------------------------------------------|
| `p_date`      | `date_t*` | 指向 `date_t` 结构体的指针，表示要减少的时间值。                       |
| `i_nb_samples`| `uint32_t`| 要减少的样本数，表示要减少的时间长度。                                 |

### 函数返回值

该函数返回减少后的时间值，类型为 `mtime_t`。返回值的具体含义如下：

- 如果 `p_date` 指向的日期成功减少 `i_nb_samples` 个样本的时间长度，则返回减少后的时间值。
- 如果 `p_date` 指向的日期为空或无效，则返回值可能为 `0` 或未定义。
## NTPtime64 {#NTPtime64}

```c
VLC_API uint64_t NTPtime64( void );
```

### 函数描述
该函数返回当前的 NTP 时间戳（64 位）。NTP 时间戳表示自 1900 年 1 月 1 日 00:00:00 UTC 以来的秒数和秒的小数部分。

### 函数参数说明
| 参数名 | 类型 | 描述 |
| ------ | ---- | ---- |
| 无     | void | 无参数 |

### 函数返回值
该函数返回一个 `uint64_t` 类型的值，表示当前的 NTP 时间戳。返回值的高 32 位表示自 1900 年 1 月 1 日 00:00:00 UTC 以来的秒数，低 32 位表示秒的小数部分。
## date_t {#date_t}

```c
struct date_t
{
    mtime_t  date;
    uint32_t i_divider_num;
    uint32_t i_divider_den;
    uint32_t i_remainder;
};
```

### 描述
`date_t` 结构体用于日期递增，避免长期递增过程中的舍入误差。

### 结构体成员说明

| 成员名          | 类型      | 描述                                                                 |
|-----------------|-----------|--------------------------------------------------------------------------|
| `date`          | `mtime_t` | 日期值，表示当前的日期。                                               |
| `i_divider_num` | `uint32_t`| 分母的分子部分，用于计算日期递增时的精确度。                           |
| `i_divider_den` | `uint32_t`| 分母的分母部分，用于计算日期递增时的精确度。                           |
| `i_remainder`   | `uint32_t`| 余数，用于在日期递增过程中保持精度，避免长期递增导致的舍入误差。       |