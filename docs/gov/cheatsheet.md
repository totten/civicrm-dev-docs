## Overview

The cheatsheet aims to summarize key information about *who* is able to
authorize *which* changes.

## Thresholds

For primary repos:

| Threshold                     | Minimum Notification  | Minimum Diversity     | Minimum Authority  |
| ----------------------------- | --------------------- | --------------------- | ------------------ |
| Non-Functional Change (NFC)   | N/A                   | Author!=Reviewer       | N/A                |
| Drop-In Change (DIC)          | N/A                   | Author!=Reviewer       | Specialist         |
| Minor Change (MNC)            | At least two relevant experts | Author!=Reviewer<br/>Author!=Authority | Fellow
| Major Change (MJC)            | All relevant experts<br/>(If none defined, then 2+ Principals)<br/>(Plus: Pre-release notice to `civicrm-dev`) |Author!=Reviewer<br/>Author!=Authority | Principal

For related repos:

| Threshold                     | Minimum Notification  | Minimum Diversity     | Minimum Authority  |
| ----------------------------- | --------------------- | --------------------- | ------------------ |
| Dictatorship                  | Relevant Principal    |                       | Relevant Principal |
| Auto-Pilot                    | N/A                   | 3x                    | Anyone             |

## Specialists

| Name                | Github               | Mattermost           | Commission                     | Git Access            |
| ------------------- | -------------------- | -------------------- | ------------------------------ | --------------------- |
| Allen Shaw          | twomice              | TwoMice              | **Comprehensive Specialist**   |
| Andrew Hunt         | agh1                 | agh1                 | **Comprehensive Specialist**   |
| Brian Shaughnessy   | lcdservices          | lcdservices          | **Comprehensive Specialist**   |
| Chris Burgess       | xurizaemon           | xurizaemon           | **Comprehensive Specialist**   | Merger, primary repos |
| Davi Alexandre      | davialexandre        | davi.alexandre       | Buildkit Specialist            | Merger, buildkit
| Deepak Srivastava   | deepak-srivastava    | deepaks              | **Comprehensive Specialist**   |
| Jamie McClelland    | jmcclelland          | jmcclelland          | **Comprehensive Specialist**   |
| Jitendra Purohit    | jitendrapurohit      | jitendrapurohit      | **Comprehensive Specialist**   |
| John Kingsnorth     | JKingsnorth          | jkingsnorth          | Dedupe Specialist              |
| John Kingsnorth     | JKingsnorth          | jkingsnorth          | Mailing Specialist             |
| Jon Goldberg        | MegaphoneJon         | junglebird           | **Comprehensive Specialist**   |
| Karin Garritsen     |                      | kgerritsen           | CiviContribute Specialist      |
| Mathieu Lutfy       | mlutfy               | bgm                  | **Comprehensive Specialist**   | Merger, everywhere    |
| Monish Deb          | monishdeb            | monish               | **Comprehensive Specialist**   | Merger, primary repos |
| Seamus Lee          | seamuslee001         | seamuslee            | **Comprehensive Specialist**   | Merger, dev-docs      |
| Yashodha Chaku      | yashodha             | yashodha             | **Comprehensive Specialist**   | Merger, primary repos |

## Fellows

| Name                | Github               | Mattermost           | Commission                     | Git Access            |
| ------------------- | -------------------- | -------------------- | ------------------------------ | --------------------- |
| Brian Shaughnessy   | lcdservices          | lcdservices          | Joomla Fellow                  |
| Chris Burgess       | xurizaemon           | xurizaemon           | Security Fellow                | Merger, primary repos |
| Christian Wach      | christianwach        | haystack             | WordPress Fellow               |
| Eileen McNaughton   | eileenmcnaughton     | eileen               | **Comprehensive Fellow**       | Merger, primary repos |
| Herb Dool           | herbdool             | herb                 | Backdrop Fellow                |
| Joe Murray          | JoeMurray            | joemurray            | CiviContribute Fellow          |
| Joe Murray          | JoeMurray            | joemurray            | CiviGrant Fellow               |
| Kevin Cristiano     | kcristiano           | kcristiano           | WordPress Fellow               |
| Mark Hanna          | jackrabbithanna      | jackrabbithanna      | Drupal Fellow                  |
| Seamus Lee          | seamuslee001         | seamuslee            | DevDocs Fellow                 | Merger, dev-docs      |

## Principals

For primary repos:

| Name                | Github               | Mattermost           | Commission                     | Git Access            |
| ------------------- | -------------------- | -------------------- | ------------------------------ | --------------------- |
| Coleman Watts       | colemanw             | coleman              | **Comprehensive Principal**    | Merger, everywhere    |
| Eileen McNaughton   | eileenmcnaughton     | eileen               | CiviContribute Principal       | Merger, primary repos |
| Eileen McNaughton   | eileenmcnaughton     | eileen               | Dedupe Principal               | Merger, primary repos |
| Mathieu Lutfy       | mlutfy               | bgm                  | Internationalization Principal | Merger, everywhere    |
| Tim Otten           | totten               | totten               | **Comprehensive Principal**    | Merger, everywhere    |

For related repos:

| Name                | Github               | Mattermost           | Commission                     | Git Access            |
| ------------------- | -------------------- | -------------------- | ------------------------------ | --------------------- |
| Alessandro Verdura  | alessandro_compucorp | alessandro_compucorp | Shoreditch Principal           | Merger, Shoreditch    |
| Deepak Srivastava   | deepak-srivastava    | deepaks              | Mosaico Principal              | Merger, primary repos and Mosaico
| Josh Gowans         |                      | josh                 | Marketing Principal            |
| Mathieu Lutfy       | mlutfy               | bgm                  | Infrastructure Principal       | Merger, everywhere    |
| Michael McAndrew    | michaelmcandrew      | michaelmcandrew      | Documentation Principal        | Merger, docs          |
| Sean Madsen         | seanmadsen           | seanmadsen           | DevDocs Principal              | Merger, dev-docs      |
