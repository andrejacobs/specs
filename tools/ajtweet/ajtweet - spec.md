# ajtweet - spec

Date: 11/05/2022

## Motivation

What is it for?

- I want to be able to send tweets without going on to twitter to do so.
- I want to be able to schedule tweets in advance. E.g. to send a tweet about recent blog posts.
- I am using this as a learning project.

Who is it for?

- The audience will just be me and perhaps someone might find the code useful to learn from as well.

How?

- I want to have a CLI written in Go that will be used to schedule the tweets as well as run on a cron/systemd schedule.
- I would also like to have a Mac app written in SwiftUI that will leverage the CLI app.

## CLI

### Adding tweets

```bash
$ ajtweet add "Send this tweet at the earliest convenience"
$ ajtweet add --at 2022-05-20T12:03:00 "This is scheduled for later"
```

### Listing tweets

```bash
$ ajtweet list
id: ba7816bf8f01cfea414140de5dae2223b00361a396177a9cb410ff61f20015ad
time: 2022-05-11T07:45:03Z00
tweet: Send this tweet at the earliest convenience

id: bef57ec7f53a6d40beb640a780a639c83bc29ac8a9816f1fc6c5c6dcd93c4721
time: 2022-05-20T12:03:00Z00
tweet: This is scheduled for later
```

### Deleting tweets

```bash
$ ajtweet delete ba7816bf8f01cfea414140de5dae2223b00361a396177a9cb410ff61f20015ad

$ ajtweet delete --all
Confirm you want to delete all tweets by entering: Lorem ipsum something generated
> Lorem ipsum something generated
```

### Sending tweets

```bash
$ ajtweet send
Sending 1 of 5
id: ba7816bf8f01cfea414140de5dae2223b00361a396177a9cb410ff61f20015ad
tweet: This is scheduled for later
...
```

### Storage

I am thinking of just storing the tweets as a JSON file.

### Configuration

Since I am planning on using Cobra, I might as well use Viper as well and allow the user to configure where the database (ahem JSON file) is stored and other properties.

### Miscellaneous

- Be able to build this for Linux and Mac.
- Need to embed the git commit and version numbers.
- Hook up GitHub actions to build and verify.
- Package up as a docker image as well?

## Next iteration

It would be a bonus if I can run a daemon `ajtweetd` as a web service that the CLI and GUI can talk to from other computers in order to manage only one database and service.