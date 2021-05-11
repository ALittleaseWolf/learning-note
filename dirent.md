
## dirent

```
<dirent函数>
opendir
readdir
每次使用readdir后，readdir会读到下一个文件，readdir是依次读出目录中的所有文件，每次只能读一个
```
```
/* 从目录中获取image_names */
std::vector<std::string>readFolder(const std::string &image_path)
{
    std::vector<std::string> image_names;
    /* dirent库函数opendir */
    auto dir = opendir(image_path.c_str());

    if ((dir) != nullptr)
    {
        struct dirent *entry;
        entry = readdir(dir);
        while (entry)
        {
            auto temp = image_path + "/" + entry->d_name;
            if (strcmp(entry->d_name, "") == 0 || strcmp(entry->d_name, ".") == 0 || strcmp(entry->d_name, "..") == 0)
            {
                entry = readdir(dir);
                continue;
            }
            image_names.push_back(temp);
            entry = readdir(dir);
        }
    }
    return image_names;
}
```
