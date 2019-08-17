---
title: "Credentials"
teaching: 10
exercises: 15
objectives:
- "Add your credentials to CERN's Gitlab"
questions:
- "How do I add my credentials?"
keypoints:
- "Use your `.ssh/gitlab` and `.ssh/gitlab.pub` keys to veryify your identy to CERN"

hidden: false
---

> ## **NOTE:** This is also documented elsewhere
>
> See [the gitlab documentation on the same topic][gitlab-keys]
{: .callout}

[gitlab-keys]: https://gitlab.cern.ch/help/ssh/README

> ## This episode assumes
>
> - You're familear with `git add` and `git commit`
> - You already have an example local repository with a README file
{: .prereq}

In this episode we'll finally get to putting something in gitlab. Of
course if you're going to put something on gitlab, you have to have a
way to convince gitlab who you are. This is where authentication comes
in.

## Authentication: Several Options

There are a few ways to authenticate yourself, each with benefits and
drawbacks.

### Passwords (`https:`)

This is probably the method you're most familiar with: every time you
interact with gitlab, you'll be prompted to enter a password. This is
the authentication method when you use "`https`" to communicate with
gitlab.

Advantages:
- Ubiquitous: everyone understands the concept
- Works anywhere (if you remember your password)
- No setup required, you just make up a password

Disadvantages:
- Annoying: especially if you use a password manager (you should) this
  will be very slow
- Accident prone: a "secret" that you type or paste a hundred times a
  day will inevitably be leaked
- Insecure: passwords always end up being leaked

### Public Key Cryptography (`ssh`)

If you don't know much about public key cryptography it's probably
worth reading the [wikipedia page on the subject][asymcrypto]. In
essence it's a bit of cryptograpic magic that enables secure
communication without ever letting your "password" leave your
laptop. Instead you'll generate a key pair: the "private" key lives on
your laptop, while the "public" one gets uploaded to gitlab.

In gitlab, this is supported via the "`ssh`" authentication method.

Advantages:
- Very secure
- Painless after the initial setup
- Second in popularity to passwords: most servers (and github) support
  this authentication method.

Disadvantages:
- Requires that you generate a key pair (one time)
- Requires you to upload a public key to gitlab
- Your private key has to accessible on your local system

Since it's more secure than passwords, automated transactions via
`ssh` aren't considered bad practice and are in fact encouraged. We'll
use this method by default since it streamlines an operation that
you'll have to do hundreds of times over the next few days.

[asymcrypto]: https://en.wikipedia.org/wiki/Public-key_cryptography

## Generating an ssh keypair

Chances are you might already have one of these pairs kicking
around. The public key usually lives in `~/.ssh/id_rsa.pub`, whereas
the private key is usually called `~/.ssh/id_rsa`. If you already have
these, you can skip to the next section.

If you don't have a keypair, you can generate one with

~~~
ssh-keygen -f ~/.ssh/id_rsa -N '' -C 'test@cern.ch'
~~~
{: .source}

If you leave off `-f` the utility will prompt you to give a location
for the file, but the default (`~/.ssh/id_rsa`) should be fine. The
`-N` option means that we won't use a password, and the `-C` option
specifies a "comment". The commnet is for your own records: using your
email address is a good way to ensure that everyone knows who it
belongs to.

Now let's look at your public key:

~~~
cat ~/.ssh/id_rsa.pub
~~~
{: .source}

should print something similar to

~~~
ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQC+AhAzgscltRnYdGI1KTz3H5jr2d/tkgmCK1GxytDYdO4HQdCOpn7pZHK1UcTScW03LrAP8Fbye+QfAVZszeiCOdMy6Emo45HjX2T2nL8zO6OxCXutruOavyFMYu4xfpZ830wJ/wLv0D58plzTrifxkzuvZEnPNr+3ytWf7jUipWbrFExcm+AfyCEc+SYnIYcp+nBlNzUKTCX06EX4uy3PFMaqaGI1+9/bckiu0QHLJei6sAHPdcv8wN18HkLqwjORmVbJOVPEsxRgTXQ35e7DQB9OBqQcEbQ2QIBMKDG7YV5yQ/0kOPbxGIGXnUoas0ZqeaK5gnAP26VlAfMeGOn5 test@cern.ch
~~~
{: .output}

Note the `test@cern.ch` at the end.

> ## Application Specific Keys
>
> We said earlier that you should never share your private key with anyone.
> This isn't always practical: sometimes you might need your private key on a server somewhere, for example.
>
> But if your private key becomes compromised, you'll have to delete your private key everywhere to make sure no steals your identy.
> You can make this slightly less likely by generating a key _just for gitlab_. Instead of using the default key location, use something like `~/.ssh/gitlab`.
> Then tell your computer to use the gitlab key when connecting to Gitlab by adding this to your `.ssh/config` file:
> ~~~
> Host gitlab.cern.ch
>  User git
>  Hostname gitlab.cern.ch
>  IdentityFile ~/.ssh/gitlab
> ~~~
> {: .source}
{: .callout}

Now that you have the keypair, we'll have to upload the _public_ key
to Gitlab.

## Uploading your public key

You can upload your key [via the gitlab interface][gitlab-key]. The
instructions there should be pretty clear: open the `.ssh/*.pub` file
with your text editor, and copy it into the "key" field. Give the key
a name that describes where it came from, i.e. "laptop ssh key".

[gitlab-key]: https://gitlab.cern.ch/profile/keys






