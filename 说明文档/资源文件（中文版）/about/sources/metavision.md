+++
date = "2017-01-01T00:00:00-04:00"
title = "MetaVision"
linktitle = "MetaVision"
weight = 2
toc = "false"

+++

MetaVision is a clinical information system provided by iMDSoft which archives and displays data at the bedside for patients cared in intensive care units at the Beth Israel Deaconness Medical Center. MIMIC-IV is solely comprised of data from Metavision. Part of the MIMIC-III database is extracted from the MetaVision system, the other part is extracted from the [CareVue system](/docs/about/sources/carevue/). The immediate consequence of this is that data for the entire duration of the MIMIC-III database needs to be extracted using special steps of different `ITEMID` in order to get data from both systems.

MetaVision is frequently referenced in the MIMIC-III documentation because:

* Patients in the MetaVision system are admitted at a later date (2008 and onward)
* Patients in the MetaVision system have data archived in a different format
* All `ITEMID` for MetaVision patients will differ from CareVue patients
