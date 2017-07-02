# Paperless

This is my attempt at having a paperless home. Over the years, I have
accumulated a pile of "important" documents that I must keep "for my records."
And yet, whenever I need a document from that pile, I can't ever find it.

[Mayan EDMS](http://mayan-edms.com) is a system to archive documents
electronically, and search them in plaintext (with the help of OCR.)

## Usage

This application is a combination of three docker images.

- [ct2p](https://hub.docker.com/coaxial/ct2p) ingests `tar.gz` archives
  containing TIFF images, runs them through a script to optimize them for OCR,
  and combines the resulting pages into a single PDF document.
- [mayan-edms](https://hub.docker.com/coaxial/mayanedms) is a [Mayan
  EDMS](http://mayan-edms.com) instance customized with extra volumes and OCR
  languages.
- [samba-dropbox](https://hub.docker.com/dperson/samba) exposes ct2p's watched
  directory as a network directory to easily copy files into the system.

### Starting up

Run `docker-compose up` and that's it.

### Updating

```
docker-compose stop &&\
docker-compose rm &&\
docker-compose pull &&\
docker-compose up
```
 will pull the latest images for every container and recreate them. Volumes
containing data are preserved during this operation and no data will be lost.
Make sure you have backups before running the command, better safe than sorry.

### Backing up

This is a manual process on the host for now. See instructions at
[coaxial/mayanedms](https://github.com/coaxial/mayanedms#backing-up). I will
eventually integrate this operation into the `docker-compose.yml` file.

## License

This project (c) coaxial 2017 under the MIT license. Included software might
have more restrictive licenses, especially for non-personal use. Please make
sure you respect their terms.
