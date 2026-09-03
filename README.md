# Passport, visa and ID photo requirements dataset

Machine-readable photo rules for 49 passport, visa and ID documents: size, head height, eye line, background, glasses and editing rules, each with the official government source it was checked against.

The data is what powers [ID Photo Maker](https://id-photo-maker.skillsafe.ai/), a free in-browser tool that crops a portrait to these sizes and prints a 4x6 or A4 sheet. Every record has a human-readable page there, for example the [U.S. passport photo](https://id-photo-maker.skillsafe.ai/us-passport-photo.html), the [Chinese passport photo](https://id-photo-maker.skillsafe.ai/china-passport-photo.html) or the [full size chart](https://id-photo-maker.skillsafe.ai/passport-photo-size-chart.html).

## Files

- `data/passport-photo-requirements.json`: the dataset with metadata (`dateModified`, `recordCount`) and a `records` array.
- `data/passport-photo-requirements.csv`: the same records, one row each; list fields are joined with ` | `.

## Fields

| Field | Meaning |
|---|---|
| `id` | short key, e.g. `us`, `us_opr`, `cn` |
| `region` | grouping used in the app's picker |
| `country` | country name |
| `documentType` | passport, visa, ID card, or a specific flow |
| `displayName` | human label |
| `format` | published size as written by the authority, e.g. `2 x 2 in`, `35 x 45 mm` |
| `widthMm` | width in millimetres (`50.8` for 2 in) |
| `heightMm` | height in millimetres |
| `digitalOnly` | `true` when the document only accepts a digital upload |
| `headHeightMinMm / headHeightMaxMm` | chin-to-crown range in mm; empty when the authority publishes none |
| `headHeightBasis` | `Officially published` or `ICAO guidance` when the authority publishes no figure |
| `eyeLineMinMm / eyeLineMaxMm` | eye line from the bottom edge, when published |
| `allowedBackgrounds / prohibitedBackgrounds` | lists of colours as the authority names them |
| `glassesRule` | `Allowed`, `Allowed if ...`, `Not allowed`, or `Not specified` |
| `editingRule` | the authority's wording on retouching and AI edits |
| `officialSource` | URL of the authority page the record was checked against |
| `lastVerified` | date the source was last read |
| `verificationStatus` | `verified` or the reason a value is missing |

## Method

Each record was read from the issuing authority's own page (the `officialSource` URL). A missing value means the authority does not publish that rule or it could not be verified from an official page. It is never a guess. Where a head-height range is not published, the record says so in `headHeightBasis` and the app falls back to ICAO Doc 9303 guidance for its guides.

Rules change. `lastVerified` is per record; open an issue if an official page now says something different, and quote the page.

## Records

| Document | Format | mm | Head height | Background | Glasses | Official source |
|---|---|---|---|---|---|---|
| United States — Passport / Visa | 2 x 2 in | 50.8 x 50.8 | 25–35 mm | white, off-white | Not allowed, except with a signed doctor's note for a documented medical reason (frames must not cover the eyes, and there must be no glare or shadow on the lenses). | [source](https://travel.state.gov/en/passports/apply/help/photos.html) |
| United States — Passport online renewal (digital photo) | Digital square image | 50.8 x 50.8 | 25–35 mm | white, off-white or cream | Not allowed | [source](https://travel.state.gov/en/passports/renew-replace/online/upload-digital-photo.html) |
| Schengen Visa / EU | 35 x 45 mm | 35 x 45 | 32–36 mm | any plain light color, light gray, gray | Allowed only with clear, untinted lenses; no glare or eye obstruction | [source](https://www.sachsen.de/en/download/plakat_Fotomustertafel.pdf) |
| United Kingdom — Passport | 35 x 45 mm | 35 x 45 | 29–34 mm | off-white or cream, light gray | Allowed only with clear, untinted lenses; no glare or eye obstruction | [source](https://www.gov.uk/photos-for-passports/photo-requirements) |
| Canada — Passport | 50 x 70 mm | 50 x 70 | 31–36 mm | not published | Not stated in reviewed source | [source](https://www.canada.ca/en/immigration-refugees-citizenship/services/canadian-passports/photos.html) |
| China — Passport / Visa | 33 x 48 mm | 33 x 48 | 30–34 mm | white, light grey, light blue | Allowed with clear, untinted lenses; frames must not obscure the eyes or show glare, and thick frames are discouraged | [source](https://www.nia.gov.cn/n741445/n763221/index.html) |
| China — Visa | 33 x 48 mm | 33 x 48 | 28–33 mm | white, close to white | Allowed if the lenses are clear and untinted, there is no glare, and the frames are not thick-rimmed or covering the eyes | [source](https://us.china-embassy.gov.cn/eng/lsfw/zj/qz2021/201612/t20161206_4410998.htm) |
| India — Passport | 35 x 45 mm | 35 x 45 | 32–36 mm | white | Allowed only with clear, untinted lenses; no glare or eye obstruction | [source](https://www.passportindia.gov.in/AppOnlineProject/pdf/ApplicationformInstructionBooklet-V3.0.pdf) |
| India — OCI card | 2 x 2 in | 50.8 x 50.8 | 25–35 mm | any plain light color | Allowed only with clear, untinted lenses; no glare or eye obstruction | [source](https://ociservices.gov.in/Photo-Spec-FINAL.pdf) |
| Argentina — DNI | 4 x 4 cm | 40 x 40 | 25–31 mm | white | Not allowed for the foto 4x4 needed at a consulate without the digital system or for an emergency passport abroad ("sin anteojos"). | [source](https://www.argentina.gob.ar/normativa/nacional/resoluci%C3%B3n-169-2011-178525/actualizacion) |
| Brazil — Passport | 50 x 70 mm | 50 x 70 | 31–36 mm | white | Not stated in reviewed source | [source](https://www.gov.br/pf/pt-br/assuntos/passaporte/ajuda/duvidas_/documentacao/documentacao-fotografia-5x7-o-que-preciso) |
| Mexico — Passport | 35 x 45 mm | 35 x 45 | 32–36 mm | white | Not allowed. The photo is taken without glasses at the appointment, and any exceptional printed photo must also be taken without glasses. | [source](https://www.gob.mx/sre/acciones-y-programas/tramite-de-pasaporte-8014) |
| Austria — Passport / ID | 35 x 45 mm | 35 x 45 | 32–36 mm | any plain light color, light gray, gray | Allowed only with clear, untinted lenses; no glare or eye obstruction | [source](https://www.bmi.gv.at/passbildkriterien/) |
| Belgium — Passport / ID | 35 x 45 mm | 35 x 45 | 31–36 mm | any plain light color | Allowed only with clear, untinted lenses; no glare or eye obstruction | [source](https://diplomatie.belgium.be/sites/default/files/2022-03/2016_matrice_nl_0.pdf) |
| Bulgaria — Passport / ID | 35 x 45 mm | 35 x 45 | 31.5–36 mm | light gray | Allowed only with clear, untinted lenses; no glare or eye obstruction | [source](https://www.mvr.bg/upload/19938/%D0%BF%D1%80%D0%B0%D0%B2%D0%B8%D0%BB%D0%BD%D0%B8%D0%BA-%D0%B7%D0%B0-%D0%B8%D0%B7%D0%B4%D0%B0%D0%B2%D0%B0%D0%BD%D0%B5-%D0%BD%D0%B0-%D0%B1%D1%8A%D0%BB%D0%B3%D0%B0%D1%80%D1%81%D0%BA%D0%B8%D1%82%D0%B5-%D0%BB%D0%B8%D1%87%D0%BD%D0%B8-%D0%B4%D0%BE%D0%BA%D1%83%D0%BC%D0%B5%D0%BD%D1%82%D0%B8-%D0%B0%D0%BA%D1%82%D1%83%D0%B0%D0%BB%D0%BD%D0%BE%D1%81%D1%82-31-05-2024.pdf) |
| Croatia — Passport / ID | 35 x 45 mm | 35 x 45 | 31.5–36 mm | any plain light color | Allowed only with clear, untinted lenses; no glare or eye obstruction | [source](https://mup.gov.hr/gradjani-281562/moji-dokumenti-281563/putovnica-330/upute-za-pripremu-fotografija-za-e-dokumente-281819/281819) |
| Czech Republic — Passport / ID | 35 x 45 mm | 35 x 45 | 32–36 mm | white, blue, light gray | Not stated in reviewed source | [source](https://mv.gov.cz/clanek/fotografie.aspx) |
| Denmark — Passport / ID | 35 x 45 mm | 35 x 45 | 30–36 mm | any plain light color | Allowed only with clear, untinted lenses; no glare or eye obstruction | [source](https://politi.dk/-/media/mediefiler/landsdaekkende-dokumenter/lov-og-information/pas/krav-til-pasfoto/krav-til-pasbilleder.pdf) |
| Finland — Passport | 36 x 47 mm | 36 x 47 | 32–36 mm | not published | Not stated in reviewed source | [source](https://poliisi.fi/documents/25235045/31329600/Passport-photograph-instructions-by-the-police-2020-EN-fixed.pdf) |
| France — Passport / ID | 35 x 45 mm | 35 x 45 | 32–36 mm | any plain light color | Allowed only with clear, untinted lenses and no glare; the frame must not be thick and must not cover the eyes. | [source](https://www.service-public.gouv.fr/particuliers/vosdroits/F10619) |
| Germany — Passport / ID | 35 x 45 mm | 35 x 45 | 32–36 mm | plain light color (ideally neutral gray), light gray for dark hair, medium gray for light hair | Allowed only with clear, untinted lenses; no glare or eye obstruction | [source](https://www.bmi.bund.de/SharedDocs/downloads/DE/publikationen/themen/moderne-verwaltung/BMI24037-fotomustertafel.html) |
| Greece — Passport | 4 x 6 cm | 40 x 60 | 31–35 mm | any plain light color, light gray | Allowed only with clear, untinted lenses; no glare or eye obstruction | [source](https://www.passport.gov.gr/en/diadikasia-ekdosis/documents/specificationphoto.html) |
| Ireland — Passport | 35 x 45 mm | 35 x 45 | 32–36 mm | light gray, white, off-white or cream | Allowed only with clear, untinted lenses; no glare or eye obstruction | [source](https://www.dfa.ie/passports/photo-guidelines/) |
| Italy — Passport / ID | 35 x 45 mm | 35 x 45 | 32–36 mm | white | Allowed only with clear, untinted lenses; no glare or eye obstruction | [source](https://www.esteri.it/en/servizi-opportunita/italiani-all-estero/documenti_di_viaggio/linee-guida-foto-icao/) |
| Netherlands — Passport / ID | 35 x 45 mm | 35 x 45 | 26–30 mm | light gray, blue, white | Allowed only with clear, untinted lenses; no glare or eye obstruction | [source](https://www.netherlandsworldwide.nl/passport-id-card/photo-requirements) |
| Norway — Passport / ID | 35 x 45 mm | 35 x 45 | 32–36 mm | not published | Not allowed | [source](https://www.politiet.no/globalassets/tjenester-admin/pass-og-id-kort/kvalitetskrav-til-passfoto.pdf) |
| Poland — Passport / ID | 35 x 45 mm | 35 x 45 | 31–36 mm | white | Allowed only with clear, untinted lenses; no glare or eye obstruction | [source](https://www.gov.pl/web/gov/zdjecie-do-dowodu-lub-paszportu) |
| Russia — Visa | 35 x 45 mm | 35 x 45 | 32–36 mm | white, off-white | Allowed only with clear, untinted lenses; no glare or eye obstruction | [source](https://evisa.kdmid.ru/) |
| Spain — Passport / DNI | 26 x 32 mm | 26 x 32 | 20–25 mm | white | Not stated in reviewed source | [source](https://www.boe.es/buscar/act.php?id=BOE-A-2005-21163) |
| Sweden — Passport / ID | 35 x 45 mm | 35 x 45 | 32–36 mm | not published | Not stated in reviewed source | [source](https://polisen.se/en/services-and-permits/passport-and-national-id-card/) |
| Switzerland — Passport / ID | 35 x 45 mm | 35 x 45 | 29–34 mm | not published | Allowed only with clear, untinted lenses; no glare or eye obstruction | [source](https://www.fedpol.admin.ch/dam/de/sd-web/ZA--3ny9zRWt/fotomustertafel.pdf) |
| Turkey — Biometric | 50 x 60 mm | 50 x 60 | 37–47 mm | white | Allowed only with clear, untinted lenses; no glare or eye obstruction | [source](https://www.nvi.gov.tr/istanbul/biyometrik-fotograf-nasil-olmalidir) |
| Ukraine — Passport / Visa | 35 x 45 mm | 35 x 45 | 32–36 mm | plain light color (published for the visa photo) | Not stated in reviewed source | [source](https://www.kmu.gov.ua/npas/249794301) |
| Australia — Passport | 35 x 45 mm | 35 x 45 | 32–36 mm | white, light gray | Not allowed | [source](https://www.passports.gov.au/help/passport-photos) |
| Hong Kong — Passport | 40 x 50 mm | 40 x 50 | 32–36 mm | white | Allowed only with clear, untinted lenses; no glare or eye obstruction | [source](https://www.immd.gov.hk/eng/residents/immigration/traveldoc/photorequirements.html) |
| Japan — Passport | 35 x 45 mm | 35 x 45 | 32–36 mm | not published | Not stated in reviewed source | [source](https://www.mofa.go.jp/mofaj/toko/passport/ic_photo.html) |
| Malaysia — Passport | 35 x 50 mm | 35 x 50 | 25–30 mm | white, off-white or cream | Not allowed | [source](https://www.kln.gov.my/documents/9375064/0/PASSPORT+PHOTO+SPECIFICATION+AND+SAMPLE+MALAYSIA.pdf/ba82dbb2-48ae-4a3e-876a-f6545b52bb4f) |
| New Zealand — Passport | 35 x 45 mm | 35 x 45 | 32–36 mm | any plain light color | Allowed only with clear, untinted lenses; no glare or eye obstruction | [source](https://www.passports.govt.nz/passport-photos) |
| Pakistan — Passport | 35 x 45 mm | 35 x 45 | 32–36 mm | white | Allowed only with clear, untinted lenses; no glare or eye obstruction | [source](https://onlinemrp.dgip.gov.pk/photo-requirements/) |
| Philippines — Passport | 35 x 45 mm | 35 x 45 | 32–36 mm | not published | Not stated in reviewed source | [source](https://ammanpe.dfa.gov.ph/86-consular-services/passports) |
| Singapore — Passport / ID | Digital photo, 400 x 514 px (print equivalent: 35 x 45 mm) | 35 x 45 | 25–35 mm | white | Allowed if the lenses are clear and untinted and the eyes are clearly visible; reflection or glare on spectacles causes rejection. | [source](https://www.ica.gov.sg/photo-guidelines) |
| South Korea — Passport | 35 x 45 mm | 35 x 45 | 32–36 mm | white | Allowed only with clear, untinted lenses; no glare or eye obstruction | [source](https://www.passport.go.kr/home/kor/contents.do?menuPos=32) |
| Taiwan — Passport / ID | 35 x 45 mm | 35 x 45 | 32–36 mm | white | Allowed only with clear, untinted lenses; no glare or eye obstruction | [source](https://www.boca.gov.tw/np-16-1.html) |
| Vietnam — Passport | 4 x 6 cm | 40 x 60 | 37–47 mm | white | Not allowed | [source](https://dichvucong.bocongan.gov.vn/bocongan/tintuc/chitiet?matin=141) |
| Israel — Passport | 35 x 45 mm | 35 x 45 | 32–36 mm | any plain light color, blue, white | Not allowed | [source](https://www.gov.il/he/pages/passport_photo_requirments_guide) |
| Morocco — Passport / ID | 35 x 45 mm | 35 x 45 | 32–36 mm | blue, white, light gray | Allowed only with clear, untinted lenses; no glare or eye obstruction | [source](https://www.passeport.ma/Home/PiecesAuMaroc) |
| Nigeria — Passport | 2 x 2 in | 50.8 x 50.8 | 25–35 mm | any plain light color, white, off-white or cream | Not allowed | [source](https://passport.immigration.gov.ng/image-compliance) |
| Saudi Arabia — Visa | 2 x 2 in | 50.8 x 50.8 | 35.6–40.6 mm | white | Not stated in reviewed source | [source](https://visa.visitsaudi.com/Home/PhotoSpecifications) |
| South Africa — Passport | 35 x 45 mm | 35 x 45 | 29–34 mm | light gray, off-white or cream | Allowed only with clear, untinted lenses; no glare or eye obstruction | [source](https://dirco.gov.za/japan/wp-content/uploads/sites/59/2024/08/Photograph-specifications-for-passports.pdf) |

## License

The dataset is released under [Creative Commons Attribution 4.0](LICENSE). Attribute as "ID Photo Maker passport photo requirements dataset, https://id-photo-maker.skillsafe.ai/". The official sources linked from each record belong to their publishers.
