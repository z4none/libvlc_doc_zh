## resolve_xml_special_chars {#resolve_xml_special_chars}

```c
VLC_API void resolve_xml_special_chars( char *psz_value );
```

### 函数描述
该函数用于解析并替换字符串中的XML特殊字符。XML特殊字符包括`&`、`<`、`>`、`'`和`"`，这些字符在XML中具有特殊含义，需要进行转义。函数会将这些特殊字符替换为对应的XML实体，例如将`&`替换为`&amp;`，将`<`替换为`&lt;`等。

### 函数参数说明

| 参数名       | 类型      | 描述                                                                 |
|--------------|-----------|--------------------------------------------------------------------|
| `psz_value`  | `char *`  | 指向需要解析和替换XML特殊字符的字符串的指针。函数会直接修改该字符串。 |

### 函数返回值
该函数没有返回值（`void`）。
## convert_xml_special_chars {#convert_xml_special_chars}

```c
VLC_API char * convert_xml_special_chars( const char *psz_content );
```

### 描述
该函数用于将字符串中的特殊字符转换为 XML 实体。例如，`<` 会被转换为 `&lt;`，`>` 会被转换为 `&gt;`，`&` 会被转换为 `&amp;`，`'` 会被转换为 `&apos;`，`"` 会被转换为 `&quot;`。

### 函数参数说明

| 参数名        | 类型        | 描述                 |
|---------------|-------------|----------------------|
| `psz_content` | `const char *` | 输入字符串，包含需要转换的特殊字符。 |

### 函数返回值
- 如果转换成功，返回一个新的字符串，其中包含转换后的 XML 实体。
- 如果输入字符串为 `NULL`，则返回 `NULL`。
- 如果内存分配失败，返回 `NULL`。

**注意**：返回的字符串需要在使用后通过 `free()` 函数释放内存。
## vlc_b64_encode_binary {#vlc_b64_encode_binary}

```c
VLC_API char * vlc_b64_encode_binary( const uint8_t *p_src, size_t i_src );
```

### 描述
该函数用于将二进制数据编码为 Base64 字符串。

### 函数参数说明

| 参数名 | 类型 | 描述 |
| --- | --- | --- |
| `p_src` | `const uint8_t *` | 指向要编码的二进制数据的指针。 |
| `i_src` | `size_t` | 要编码的二进制数据的长度。 |

### 函数返回值
- 成功时，返回一个指向 Base64 编码字符串的指针。
- 如果编码失败，返回 `NULL`。
## vlc_b64_encode {#vlc_b64_encode}

```c
VLC_API char * vlc_b64_encode( const char * );
```

### 描述
该函数用于将输入的字符串进行 Base64 编码。Base64 编码是一种将二进制数据转换为 ASCII 字符串的方法，常用于在文本协议中传输二进制数据。

### 函数参数说明

| 参数名 | 类型 | 描述 |
| --- | --- | --- |
| `input` | `const char *` | 需要进行 Base64 编码的输入字符串。 |

### 函数返回值
- **成功**：返回一个指向 Base64 编码后字符串的指针。该字符串是动态分配的，调用者需要在使用完毕后调用 `free()` 函数释放内存。
- **失败**：返回 `NULL`，表示编码过程中发生了错误。
## vlc_b64_decode_binary_to_buffer {#vlc_b64_decode_binary_to_buffer}

```c
VLC_API size_t vlc_b64_decode_binary_to_buffer( uint8_t *p_dst, size_t i_dst_max, const char *psz_src );
```

### 函数描述
该函数用于将 Base64 编码的字符串解码为二进制数据，并将结果存储在指定的缓冲区中。

### 函数参数说明

| 参数名       | 类型          | 描述                                                                 |
|--------------|---------------|--------------------------------------------------------------------------|
| `p_dst`      | `uint8_t *`   | 指向目标缓冲区的指针，用于存储解码后的二进制数据。                       |
| `i_dst_max`  | `size_t`      | 目标缓冲区的最大容量，即缓冲区可以存储的最大字节数。                     |
| `psz_src`    | `const char *`| 指向 Base64 编码字符串的指针，该字符串将被解码为二进制数据。             |

### 函数返回值
- 如果解码成功，返回写入目标缓冲区的字节数。
- 如果目标缓冲区不足以存储解码后的数据，返回 `(size_t)-1`。
## vlc_b64_decode_binary {#vlc_b64_decode_binary}

```c
VLC_API size_t vlc_b64_decode_binary( uint8_t **pp_dst, const char *psz_src );
```

### 描述
该函数用于将 Base64 编码的字符串解码为二进制数据。解码后的二进制数据存储在 `pp_dst` 指向的内存中，该内存由函数自动分配。

### 函数参数说明

| 参数名   | 类型        | 描述                                                                 |
|----------|-------------|--------------------------------------------------------------------|
| `pp_dst` | `uint8_t **`| 指向解码后的二进制数据的指针。函数会分配内存并将指针存储在 `*pp_dst` 中。 |
| `psz_src`| `const char *` | 指向要解码的 Base64 编码字符串的指针。                                |

### 函数返回值
- 返回值为解码后的二进制数据的长度（以字节为单位）。
- 如果解码失败（例如输入字符串不是有效的 Base64 编码），则返回 `0`，并且 `*pp_dst` 将被设置为 `NULL`。
## vlc_b64_decode {#vlc_b64_decode}

```c
VLC_API char * vlc_b64_decode( const char *psz_src );
```

### 描述
该函数用于将 Base64 编码的字符串解码为原始字符串。

### 函数参数说明

| 参数名    | 类型        | 描述                   |
|-----------|-------------|------------------------|
| `psz_src` | `const char *` | 指向 Base64 编码字符串的指针 |

### 函数返回值
- **成功**：返回指向解码后的字符串的指针。
- **失败**：返回 `NULL`，表示解码失败。
## str_format_time {#str_format_time}

```c
VLC_API char * str_format_time( const char * );
```

### 描述
该函数用于将时间格式化为字符串。它接受一个时间字符串作为输入，并返回一个格式化后的时间字符串。

### 函数参数说明

| 参数名 | 类型 | 描述 |
|--------|------|------|
| `time` | `const char *` | 输入的时间字符串，通常是一个表示时间的字符串。 |

### 函数返回值
- 如果成功，返回一个格式化后的时间字符串。
- 如果输入的时间字符串无效或格式不正确，返回 `NULL`。
## str_format_meta {#str_format_meta}

```c
VLC_API char * str_format_meta( input_thread_t *p_input, const char *psz_meta );
```

### 描述
该函数用于格式化元数据字符串。它接受一个输入线程对象和一个元数据字符串，并返回一个格式化后的字符串。

### 函数参数说明

| 参数名       | 类型               | 描述                                                                 |
|--------------|--------------------|--------------------------------------------------------------------------|
| `p_input`    | `input_thread_t *` | 指向输入线程对象的指针，用于获取相关的元数据信息。                       |
| `psz_meta`   | `const char *`     | 指向要格式化的元数据字符串的指针。                                       |

### 函数返回值
- 成功时，返回一个指向格式化后的字符串的指针。
- 如果输入线程对象或元数据字符串为空，或者格式化过程中发生错误，则返回 `NULL`。
## free {#free}

```c
void free(void *s1);
```

### 描述
`free` 函数用于释放之前通过 `malloc`、`calloc` 或 `realloc` 函数分配的内存空间。调用 `free` 后，指向该内存的指针将变为无效，不应再使用。

### 函数参数说明

| 参数 | 类型 | 描述 |
|------|------|------|
| `s1` | `void *` | 指向要释放的内存块的指针。 |

### 函数返回值
`free` 函数没有返回值。
## filename_sanitize {#filename_sanitize}

```c
VLC_API void filename_sanitize( char * );
```

### 描述
该函数用于对文件名进行清理，以确保文件名符合操作系统的要求。它会移除或替换文件名中的非法字符，以避免在创建文件时出现问题。

### 函数参数说明

| 参数名 | 类型 | 描述 |
|--------|------|------|
| `char *` | 输入/输出 | 指向需要进行清理的文件名字符串的指针。函数会直接修改该字符串。 |

### 函数返回值
该函数没有返回值。
## path_sanitize {#path_sanitize}

```c
VLC_API void path_sanitize( char * );
```

### 函数描述
`path_sanitize` 函数用于清理和规范化给定的路径字符串。它确保路径中的所有字符都是有效的，并且路径符合文件系统的要求。

### 函数参数说明

| 参数名 | 类型 | 描述 |
|--------|------|------|
| `char *` | `path` | 指向需要清理和规范化的路径字符串的指针。 |

### 函数返回值
该函数没有返回值。它直接修改传入的路径字符串，使其符合规范。
## str_duration {#str_duration}

```c
VLC_API time_t str_duration(const char *psz_duration);
```

### 函数描述
该函数将一个表示时间的字符串转换为 `time_t` 类型的值。字符串可以表示为小时、分钟、秒或毫秒的组合。

### 函数参数说明

| 参数名          | 类型        | 描述                                                                 |
|-----------------|-------------|--------------------------------------------------------------------------|
| `psz_duration`  | `const char *` | 表示时间的字符串，格式可以是 `HH:MM:SS`、`MM:SS`、`SS` 或 `SS.ms` 等。 |

### 函数返回值
- 如果转换成功，返回转换后的 `time_t` 值，表示时间的长度（以秒为单位）。
- 如果输入字符串格式不正确或转换失败，返回 `0`。