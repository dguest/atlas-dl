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

> ## **NOTE:** we probably don't need this section
>
> This could be replaced by [the gitlab documentation on the same topic][gitlab-keys]
{: .callout}

[gitlab-keys]: https://gitlab.cern.ch/help/ssh/README

> ## This episode assumes
>
> - You're familear with `git add` and `git commit`
> - You already have an example local repository with a README file
{: .prereq}

In this episode we'll finally get to putting something in gitlab

## Aside: passwords are terrible security

If you're like most people, when you think of authentication you think
of passwords. This is probably owing to their visibility: the concept
behind them isn't hard to understand, and you probalby have to type
them in several times a day.

But passwords are terrible. They are annoying to type, (relatively)
easy to guess, prone to errors, and password reuse is probably the
single biggest cause of those massive security breaches you learn
about on the news.

Without getting into all the details of
[public key cryptography][asymcrypto], there's a _much more secure_
way to authenticat yourself. The idea is pretty awesome:

  - You create an **assymetric** key _pair_, A and B. These are magic
    little one-way pipes: you can encrypt something with A and _no
    one_ can decrypt it without B, _even if they have_ A. Conversely,
    if you encrypt something with B _no one_ can decrypt it without A,
    even if they have B.

    If you're used to reversable processes from physics class, this
    idea might make your head hurt. Don't worry; it's weird but, it
    works.

  - You call one of these your "public" key. You can share this with
    anyone or everyone. The other one becomes your "private" key,
    **you never share this with anyone**, it just lives on your
    computer.

The neat thing about this system is that it gives _everyone_ a way to
verify that they are in fact talking to _you_.

But to get back to our lesson: say you want to push some information to
gitlab. Obviously we want to make sure gitlab knows who you are so
some stranger isn't pushing to _your_ repository.

While it's an oversimplification, the exchange looks _something_ like
this:

0. You generate a key pair, and share your public key with gitlab. Again you **never** share your private key with anyone.
1. Gitlab uses your public key and encrypts a short message, maybe
   something like "I ate 45 donkeys for lunch"
2. Gitlab sends you the _encrypted_ message.
3. You decrypt it _with your private key_ and send the unencrypted
   message back.
4. If gitlab sees "I ate 45 donkeys for lunch" (the same thing they
   generated), they let you push your code. If, on the other hand,
   someone else is _pretending_ to be you, gitlab will see a message
   more like "ebcf7a633f0e2487621cb611c2"
5. The next time you communicate with Gitlab, they will encrypt
   something else, i.e. "I ate 46 donkeys for lunch"

The beauty here is that you _never_ had to share anything sensitive
with gitlab, but they can still verify your identiy. Also, since there
are no passwords (only keys on computers) the whole process can be
automated!

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

### Testing your key

(note from Dan: this needs to be tested)

You can confirm that your key is working by running

~~~
ssh -T git@gitlab.cern.ch
~~~
{: .source}






