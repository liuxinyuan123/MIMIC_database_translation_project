---
title: "services"
linktitle: "services"
weight: 1
date: 2020-08-10
description: >
  The hospital service(s) which cared for the patient during their hospitalization.
---

## *services*

*services* 表描述了患者入院时所接受的服务。虽然患者可能位于某种 ICU 类型（例如 MICU），但他们不一定由 MICU 的团队护理。这可能是由于多种原因造成的，包括床位短缺。如果对识别患者在医院接受的服务类型感兴趣，应使用 *services* 表。例如，如果对识别手术患者感兴趣，推荐的方法是搜索在手术服务下入院的患者。


每个服务在表中都以缩写形式列出 - 这正是数据在医院数据库中的存储方式。为了方便用户，我们提供了每种服务类型的描述。

| Service | Description                                                                                                                          |
|---------|--------------------------------------------------------------------------------------------------------------------------------------|
| CMED    | Cardiac Medical - for non-surgical cardiac related admissions                                                                        |
| CSURG   | Cardiac Surgery - for surgical cardiac admissions                                                                                    |
| DENT    | Dental - for dental/jaw related admissions                                                                                           |
| ENT     | Ear, nose, and throat - conditions primarily affecting these areas                                                                   |
| EYE     | Eye diseases - including subspecialty services in glaucoma, cataract surgery, cornea and external diseases, and neuro-ophthalmology. |
| GU      | Genitourinary - reproductive organs/urinary system                                                                                   |
| GYN     | Gynecological - female reproductive systems and breasts                                                                              |
| MED     | Medical - general service for internal medicine                                                                                      |
| NB      | Newborn - infants born at the hospital                                                                                               |
| NBB     | Newborn baby - infants born at the hospital                                                                                          |
| NMED    | Neurologic Medical - non-surgical, relating to the brain                                                                             |
| NSURG   | Neurologic Surgical - surgical, relating to the brain                                                                                |
| OBS     | Obstetrics - conerned with childbirth and the care of women giving birth                                                             |
| ORTHO   | Orthopaedic - surgical, relating to the musculoskeletal system                                                                       |
| OMED    | Oncologic Medical - non-surgical, relating to cancer                                                                                 |
| PSURG   | Plastic - restortation/reconstruction of the human body (including cosmetic or aesthetic)                                            |
| PSYCH   | Psychiatric - mental disorders relating to mood, behaviour, cognition, or perceptions                                                |
| SURG    | Surgical - general surgical service not classified elsewhere                                                                         |
| TRAUM   | Trauma - injury or damage caused by physical harm from an external source                                                            |
| TSURG   | Thoracic Surgical - surgery on the thorax, located between the neck and the abdomen                                                  |
| VSURG   | Vascular Surgical - surgery relating to the circulatory system                                                                       |

## 表连接

* patients on `subject_id`
* admissions on `hadm_id`

<!-- # Important considerations -->

## 表列描述

| Name           | Postgres data type |
|----------------|--------------------|
| `subject_id`   | INT                |
| `hadm_id`      | INT                |
| `transfertime` | TIMESTAMP(0)       |
| `prev_service` | VARCHAR(20)        |
| `curr_service` | VARCHAR(20)        |

### `subject_id`

### `hadm_id`

## `transfertime`

`transfertime` 是患者从 `prev_service`（如果存在）转移到 `curr_service` 的时间。

## `prev_service`, `curr_service`

`prev_service` 和 `curr_service` 是患者之前和当前所接受的服务。
