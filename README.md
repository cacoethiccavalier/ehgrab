# EHgrab

A shell scrip to download all images from an E-Hentai gallery

## Installation

### Dependencies

EHgrab is a fairly simple script making use of standard Unix utilities (`curl`, `sed`, `grep`, `echo`, etc.) which should be available in most Unix terminals. If you encounter a situation in which this is not the case, let me know in an issue, and I'll make a note for future users.

### Installing

Place the `ehgrab` file anywhere you'd like. Place it in a directory on your `PATH` if you'd like easy access.

### Setting Up Environment Variables.

EHgrab makes use of a few environment variables for ease of use.

####EHUSR and EHPWD

`EHUSR` and `EHPWD` are optional environment variables that hold your E-Hentai username and password hash, respectively. These are used in the cookies of HTTP requests used to get high quality images, since the high quality image download feature is only available to registered users. If you're satisfied with standard quality images (max 1280px x 1280px), you can still use EHgrab without these environment variables, and it will download the standard quality images.

To find out what these values should be, enter `document.cookie` in your browser's console and look for the keys `ipb_member_id` and `ipb_pass_hash`. Set `EHUSR` to the value of the former and `EHPWD` to the value of the latter.

####EHDEST

`EHDEST` is an optional environment variable that holds the default download location for images. This can be overridden by providing a destination path at execution, and does not need to be included if such a path is provided.

## Usage

Use EHgrab from the terminal like so:
```
ehgrab url [path]
```

`url` should be the URL of the gallery page of the gallery you would like to download. That is, the page that shows the gallery's first image, meta-data, tags, and thumbnails of the first set of images.

`path` should be the path to the directory in which you would like EHgrab to place the downloaded images. This is optional if you have set the `EHDEST` environment variable.

## Reporting Issues and Contributing

EHgrab is a somewhat fragile script that works by making assumptions about E-Hentai's gallery page structure. If things change, it will likely break. It would be a big help if you report any bugs you encounter by opening an issue.

If you have any features you'd like to see added, open an issue and I'll see what I can do.

If you'd like to contribute something, open a pull request, or contact me via email.
