# backup_tumblr

This is a set of scripts for downloading your posts and likes from Tumblr.

The scripts try to download as much as possible, including:

*   Every post and like
*   All the metadata about a post that's available through the Tumblr API
*   Any media files attached to a post (e.g. photos, videos)

I've had these for private use for a while, and in the wake of Tumblr going on a deletion spree, I'm trying to make them usable by other people.

**If you're having problems, the easiest way to get my attention is by [opening an issue](https://github.com/alexwlchan/backup_tumblr/issues/new).**
If you don't have a GitHub account, there are alternative contact details [on my website](https://alexwlchan.net/contact/).

![](stampede_400.jpg)

<sup>Pictured: a group of Tumblr users fleeing the new content moderation policies. Image credit: <a href="https://wellcomecollection.org/works/depa2hf5">Wellcome Collection</a>, CC BY.</sup>

## Motivation

**These scripts are only for personal use.**
Please don't use them to download posts and then make them publicly accessible without consent.
Your own blog is yours to do what you want with; your likes and other people's posts are not.

Some of what's on Tumblr is deeply personal content, and is either private or requires a login.
Don't put it somewhere where the original creator can't control how it's presented or whether it's visible.

## Getting started

1.  Install Python 3.6 or later.
    Instructions on [the Python website](https://www.python.org/downloads/).

2.  Check you have pip installed by running the following command at a command prompt:

    ```console
    $ pip3 --version
    pip 18.1 (python 3.6)
    ```

    If you don't have it installed or the command errors, follow the [pip installation instructions](https://pip.pypa.io/en/stable/installing/)

3.  Clone this repository:

    ```console
    $ git clone https://github.com/alexwlchan/backup_tumblr.git
    $ cd backup_tumblr
    ```

4.  Install the Python dependencies:

    ```console
    $ pip3 install -r requirements.txt
    ```

5.  Get yourself a Tumblr API key by registering an app at <https://www.tumblr.com/oauth/apps>.

    If you haven't done it before, start by clicking the **Register application** button:

    ![](register_application.png)

    Then fill in the details for your app.
    Here's an example of what you could use (but put your own email address!):

    ![](api_registration.png)

    You can leave everything else blank.
    Then scroll down and hit the "Register" button.

    ![](rate_limits.png)

    Note: unless you have a _lot_ of posts (20k or more), you shouldn't need to ask for a rate limit removal.

    Once you've registered, you'll have a new entry in the list of applications.
    You need the **OAuth Consumer Key**:

    ![](tumblr_api_key.png)

## Usage

There are three scripts in this repo:

1.  `save_posts_metadata.py` saves metadata about all the posts on your blog.
2.  `save_likes_metadata.py` saves metadata about all the posts you've liked.
3.  `save_media_files.py` saves all the media (images, videos, etc.) from those posts.

They're split into separate scripts because saving metadata is much faster than media files.

You should run (1) and/or (2), then run (3).
Something like:

```console
$ python3 save_posts_metadata.py

$ python3 save_likes_metadata.py

$ python3 save_media_files.py
```

If you know what command-line flags are: you can pass arguments (e.g. API key) as flags.
Use `--help` to see the available flags.

If that sentence meant nothing: don't worry, the scripts will ask you for any information they need.

## Unanswered questions and notes

*   I have no idea how Tumblr's content blocks interact with the API, or if blocked posts are visible through the API.

*   I've seen mixed reports saying that ordering in the dashboard has been broken for the last few days.
    Again, no idea how this interacts with the API.

*   Media files can get big.
    I have ~12k likes which are taking ~9GB of disk space.
    The scripts will merrily fill up your disk, so make sure you have plenty of space before you start!

*   These scripts are provided "as is".
    File an issue if you have a problem, but I don't have much time for maintenance right now.

*   Sometimes the Tumblr API claims to have more posts than it actually returns, and the effect is that the script appears to stop early, e.g. at 96%.

    I'm reading the `total_posts` parameter from the API responses, and paginating through it as expected -- I have no idea what causes the discrepancy.

## Alternatives

These scripts only save the raw API responses and media files.

It *doesn't* create a pretty index, or interface, or make it especially searchable.
I like saving the complete response because it gives me as much flexibility as possible, but it means you need more work to do something useful later.

If you're looking for a more full-featured, well-documented project, I've heard good things about [bbolli/tumblr-utils](https://github.com/bbolli/tumblr-utils).

## Acknowledgements

Hat tip to [@cesy](https://github.com/cesy/) for nudging me to post it, and providing useful feedback on the initial version.

## Licence

MIT.
