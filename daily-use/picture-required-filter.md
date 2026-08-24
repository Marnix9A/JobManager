# Picture Required (filter)

A filter can be specified here which determines which files are accepted in for [Picture required](./picture-required.md).

The filter is specified as a text. Below are a few examples:

*   `Image` indicates that only images are accepted (jpeg, jpg etc.).
*   `PDF` indicates that only PDF is accepted.
*   `Image|PDF` indicates that both images and PDF are accepted.

The allowed values ​​must match the values ​​in [Type](../all-tables/type-7.md) on [JobManager Attachments](../all-tables/jobmanager-attachment.md).

If working with the same questions in different BC/NAV language the filters should be applied as the numbers: `2` for Images, `3` for PDF etc.
