# ggplot

## Wrong image DPI

When an image is saved via `tiff()` or other similar functions, the DPI is saved in the metadata of the file. The macos previewer however cannot read the metadata correctly, showing 72 DPI no matter what the output DPI is.

Sources:
https://stackoverflow.com/questions/70309119/why-am-i-not-getting-high-resolution-with-ggsave

