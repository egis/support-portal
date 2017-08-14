## Properties

| Property                                 | Description                           | Default                                  |
| ---------------------------------------- | ------------------------------------- | ---------------------------------------- |
| action.download.order.links              |                                       |                                          |
| actions.email.default.bcc                |                                       |                                          |
| actions.email.record.body                |                                       | false                                    |
| actions.notify.from.user                 |                                       |                                          |
| authentication.otp.provider              |                                       |                                          |
| authentication.user.provider             |                                       |                                          |
| autoExport.imagify.resolution            |                                       |                                          |
| autonumber.increment                     |                                       | 1                                        |
| autonumber.offset                        |                                       | 1                                        |
| branch.enable                            |                                       |                                          |
| branch.upstream                          |                                       |                                          |
| bulk.download.max                        |                                       |                                          |
| captcha.on.login.attempts                |                                       | 0                                        |
| captcha.on.password.reset                |                                       |                                          |
| cluster.enable                           |                                       |                                          |
| cluster.ip                               |                                       |                                          |
| cluster.multicast                        |                                       |                                          |
| cluster.name                             |                                       |                                          |
| cluster.password                         |                                       |                                          |
| conversion.engine.disabled.ext           |                                       |                                          |
| conversion.engine.retry                  |                                       | 2                                        |
| conversion.engine.threads                |                                       | 1                                        |
| conversion.engine.timeout                |                                       | 30000                                    |
| conversion.openoffice.connection.timeout |                                       | 15000                                    |
| conversion.openoffice.path               |                                       |                                          |
| conversion.remote.host                   |                                       |                                          |
| cookie.fqdn.domain                       |                                       |                                          |
| cookie.httpOnly                          |                                       |                                          |
| cookie.secure                            |                                       |                                          |
| date.format                              |                                       |                                          |
| db.auto.warm                             |                                       |                                          |
| db.backup.dir                            |                                       | default_file_store                       |
| db.database                              |                                       | transnet_pt                              |
| db.debug                                 |                                       | false                                    |
| db.host                                  |                                       |                                          |
| db.pass                                  |                                       |                                          |
| db.pool.max.wait                         |                                       |                                          |
| db.pool.size.max                         |                                       |                                          |
| db.pool.size.min                         |                                       |                                          |
| db.pool.test.on.borrow                   |                                       |                                          |
| db.pool.test.on.return                   |                                       |                                          |
| db.pool.timeout                          |                                       |                                          |
| db.port                                  |                                       |                                          |
| db.type                                  |                                       |                                          |
| db.url.config                            |                                       |                                          |
| db.user                                  |                                       |                                          |
| disable.custom.stores                    |                                       |                                          |
| disabled.actions                         |                                       | none                                     |
| disabled.entity.audits                   |                                       |                                          |
| document.integrity.schedule.fix          |                                       | false                                    |
| document.preview.swf                     |                                       | true                                     |
| email.audit.verbose                      |                                       |                                          |
| email.error.verbose                      |                                       |                                          |
| email.import.error.node                  |                                       | System/email/errors                      |
| email.preview.force                      |                                       | true                                     |
| email.preview.threads                    |                                       | false                                    |
| extract.file.metadata                    |                                       | true                                     |
| file.garbage.collection.enable           |                                       | true                                     |
| file.replication.upstream                |                                       |                                          |
| ftp.enable                               |                                       | false                                    |
| ftp.passive.address                      |                                       |                                          |
| ftp.passive.external.address             |                                       |                                          |
| ftp.passive.ports                        |                                       | 64000-65000                              |
| ftp.port                                 |                                       | 21                                       |
| ftp.timeout                              |                                       | 300                                      |
| gelf.host                                |                                       |                                          |
| gelf.level                               |                                       |                                          |
| grid.export.exclude.columns              |                                       | hasNotes,hasLinks,hasAttachments,contentIcon,imageIcon,status |
| group.sync.ds                            |                                       |                                          |
| group.sync.interval                      |                                       | 0                                        |
| group.sync.removeGroups                  |                                       | false                                    |
| health.password                          |                                       |                                          |
| health.report.checks                     |                                       |                                          |
| health.report.url                        |                                       |                                          |
| http.hostname                            |                                       |                                          |
| http.log                                 |                                       |                                          |
| http.port                                |                                       | 8080                                     |
| http.session.timeout                     |                                       | 7200                                     |
| http.ssl.client.require                  |                                       | false                                    |
| http.ssl.force                           |                                       | true                                     |
| http.ssl.password                        |                                       |                                          |
| http.ssl.port                            |                                       | 8443                                     |
| http.ssl.trustPassword                   |                                       |                                          |
| http.ssl                                 |                                       | false                                    |
| import.service.threads                   |                                       | 2                                        |
| index.allow.leading.wild.card            |                                       |                                          |
| index.backup.dir                         |                                       |                                          |
| index.commit.interval                    |                                       | 1                                        |
| index.dir                                |                                       |                                          |
| index.disable                            |                                       |                                          |
| index.force.index.open                   |                                       | true                                     |
| index.full.text.disable                  |                                       | false                                    |
| index.full.text.ext.disable              |                                       |                                          |
| index.full.text.size.disable             |                                       | 10240                                    |
| index.max.results                        |                                       | 100000                                   |
| index.rebuild.threads                    |                                       | 1                                        |
| index.refresh.interval                   |                                       | 1                                        |
| index.store                              |                                       | false                                    |
| index.updater.batch.size                 |                                       |                                          |
| index.upstream                           |                                       |                                          |
| jar.disable                              |                                       | false                                    |
| key.store.password                       |                                       |                                          |
| ldap.account.lookup.query                |                                       | (&(objectClass=user)(mail=*)(            |
| ldap.context.name                        |                                       |                                          |
| ldap.domain                              |                                       | inter.transnet.net                       |
| ldap.host                                |                                       | 10.98.227.113                            |
| ldap.pass                                |                                       | Yk.12345                                 |
| ldap.port                                |                                       | 389                                      |
| ldap.skip.verification                   |                                       | false                                    |
| ldap.ssl                                 |                                       | false                                    |
| ldap.sync.groups                         |                                       | false                                    |
| ldap.user.autoCreate                     |                                       | false                                    |
| ldap.user.format                         |                                       |                                          |
| ldap.user                                |                                       | 9994160                                  |
| ldap.verify.user                         |                                       | 9994160                                  |
| license                                  |                                       | *#Egis#1000#standard,portal=1000,scanner=3,workflow=true,clustering=true,capture=true,esign=true,api=true,all=true#ed97c0c6 |
| list.index.search.max.results            |                                       |                                          |
| log.files.purge.age                      |                                       | 720                                      |
| messaging.journal.disable                |                                       |                                          |
| metadata.field.permissions               |                                       | true                                     |
| monitoring.enable                        |                                       | false                                    |
| node.creation.timeout                    |                                       |                                          |
| opensearch.guest.user                    |                                       |                                          |
| party.autocomplete.results               |                                       |                                          |
| pbkdf2.iterations                        |                                       |                                          |
| pdf.export.font                          |                                       | Helvetica                                |
| pdf.export.header.color                  |                                       | C3DAF9                                   |
| pdf.export.margins                       |                                       | 15                                       |
| pdf.export.max.portrait.cols             |                                       | 4                                        |
| pdf.export.med.font.size                 |                                       | 8                                        |
| pdf.export.small.font.size.cols          |                                       | 10                                       |
| pdf.export.small.font.size               |                                       | 6                                        |
| postprocess.imagify.resolution           |                                       |                                          |
| preprocess.timeout                       |                                       | 5000                                     |
| quick.search.default.filter              |                                       | startsWith                               |
| recycle.bin.enable                       |                                       | true                                     |
| remember.me.age                          |                                       | 14                                       |
| replication.increment                    |                                       |                                          |
| replication.offset                       |                                       |                                          |
| replication.upstream                     |                                       |                                          |
| reseed.db                                |                                       |                                          |
| saml.idp.url                             |                                       |                                          |
| saml.mapping.expression                  |                                       | NameID                                   |
| saml.private.key                         |                                       |                                          |
| saml.public.key                          |                                       | saml-public.key                          |
| scheduled.report.prefix                  |                                       |                                          |
| scheduler.thread.pool.size               |                                       |                                          |
| security.level                           |                                       | Low                                      |
| signature.api.key                        |                                       |                                          |
| signature.audit.page.disable             |                                       | false                                    |
| signature.authentication.disable         |                                       | true                                     |
| signature.certificate.format             |                                       | ${reason?Digitally Signed} by ${user<br>${datetime} |
| signature.certificate.password           |                                       |                                          |
| signature.certificate.path               |                                       |                                          |
| signature.format                         |                                       | ${title?};EMP NO. ${login?}              |
| signature.reason.font                    |                                       | Times New Roman; 14; 061738              |
| signature.script.font                    | Force a specific signature font style | 1; 20; ff0000                            |
| signature.text.font                      |                                       | Times New Roman; 12; #5c595e             |
| signature.tsa.password                   |                                       |                                          |
| signature.tsa.url                        |                                       |                                          |
| signature.tsa.username                   |                                       |                                          |
| signature.upload.http                    |                                       |                                          |
| signature.upload.node                    |                                       | signature uploads                        |
| signup.enabled                           |                                       | true                                     |
| sms.country.code                         |                                       | 27                                       |
| sms.extra                                |                                       | &api_id=                                 |
| sms.from                                 |                                       |                                          |
| sms.pass                                 |                                       | ****                                     |
| sms.url                                  |                                       | http://api.clickatell.com/http/sendmsg?user=${sms.user}&password=${sms.pass}${sms.extra}&to=${to}&text=${message} |
| sms.user                                 |                                       |                                          |
| smtp.debug                               |                                       | false                                    |
| smtp.disable                             |                                       | false                                    |
| smtp.from                                |                                       | noreply@egis-software.com                |
| smtp.host                                |                                       |                                          |
| smtp.pass                                |                                       | ****                                     |
| smtp.port                                |                                       |                                          |
| smtp.sentItemsThreading                  |                                       | false                                    |
| smtp.sentItems                           |                                       | false                                    |
| smtp.server.enable                       |                                       | false                                    |
| smtp.server.incoming                     |                                       | Incoming SMTP                            |
| smtp.server.port                         |                                       | 3025                                     |
| smtp.ssl.port                            |                                       |                                          |
| smtp.ssl                                 |                                       | false                                    |
| smtp.tls                                 |                                       | false                                    |
| smtp.user                                |                                       |                                          |
| spnego.debug                             |                                       |                                          |
| spnego.domain                            |                                       |                                          |
| spnego.enable                            |                                       | false                                    |
| spnego.kdc                               |                                       |                                          |
| spnego.krb5.conf                         |                                       |                                          |
| spnego.login.conf                        |                                       |                                          |
| spnego.pass                              |                                       |                                          |
| spnego.principal                         |                                       |                                          |
| spnego.user                              |                                       |                                          |
| storage.processing.threads               |                                       |                                          |
| storage.verify                           |                                       |                                          |
| strip.stack.traces                       |                                       |                                          |
| summary.column.width                     |                                       | 100                                      |
| support.email                            |                                       | support@egis-software.com                |
| support.phone                            |                                       | +27 11 880 4411                          |
| support.showStackTraces                  |                                       | true                                     |
| system.mode                              |                                       |                                          |
| task.reporter.url                        |                                       |                                          |
| temp.dir.purge.age                       |                                       | 2                                        |
| ui.capture.document.types                |                                       |                                          |
| ui.emailReplyTo                          |                                       | To Field + User Name                     |
| ui.rememberMe                            |                                       | true                                     |
| ui.resetPassword                         |                                       | true                                     |
| user.default.password                    |                                       | papertrail                               |
| user.reset.email                         |                                       | true                                     |
| waffle.enable                            |                                       | false                                    |
| web.login.page                           |                                       | /web/webapps/login.html                  |
| web.login.sms.otp.text                   |                                       | PIN for papertrail is: ${otp}            |
| web.login.sms.otp                        |                                       |                                          |
| web.main.page                            |                                       | /web/portal                              |
| web.root.page                            |                                       | /web/webapps/main.html                   |
