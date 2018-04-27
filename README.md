# findcontact

Find contacts (vcards) from a given .vcf file

Hosted at https://git.faster-it.com/findcontact    
Mirrored at https://github.com/fasterit/findcontact    

## About

**findcontact** is a small perl script that enables searching with a set of regexes to find contacts within a (large) .vcf file.

Obtaining a contacts.vcf depends on which CardDAV server / client you run.    
With [radicale](http://radicale.org/) you can just copy the file off the server into the directory where your findcontact resides. Or copy / link findcontact into the correct radicale collections subdirectory.

Unfortunately every .vcf client decides on a specific set of attributes to support and the [Inverse Sogo Connector](https://sogo.nu/download.html#/frontends) everybody uses for getting the Thunderbird address book synced can't search over all fields. So if you want to search for a phone number you're out of luck. Unless you run findcontact :).

It has been written to only depend on perl modules that ship with a default installation and does __not__ depend on Text::vCard::Addressbook or the like.

## License

The script is licensed under the [MIT license](https://opensource.org/licenses/MIT).

## Installation

Clone this repository and **copy** or **symlink** `findcontact` to the directory where your `contacts.vcf` file resides. The name is hard-coded as that is what we use inside Faster IT GmbH and it's customary for collections of vcards. Obviously if your organizations does differently, change the $contacts_file line.

This script requires perl and runs under Linux, MacOSX and Windows/cygwin.
It assumes Linux line endings in the `contacts.vcf` file (\n only). We never saw anything different but if you run MacOSX server ... you may have to adopt the script a bit.

## Usage

`findcontact` takes an arbitrary number of arguments which are all regexes. All of the arguments given must match to have a vcard shown. All matches are case-insensitive.

Thus you can easily iterate:

    $ findcontact pizza
    $ findcontact pizza "m(ü|ue)nchen"
    $ findcontact pizza "m(ü|ue)nchen" schwabing

All fields are searched, so you can also search for phone numbers or parts of the comment field:

    $ findcontact "89.*4209"

If you want to limit the fields printed, use grep:

    $ findcontact pizza | grep "^\(FN\|TEL\|$\|Found \)"

Inside `findcontact` you'll find that the `VERSION`, `PRODID`, `PHOTO`, `UID` and `X-RADICALE-NAME` fields are removed from the output. If you need any of them or want to always remove further fields from output ... change the appropriate lines.

## Support

Commercial support is available from Faster IT GmbH.
