# Spendula — Privacy Policy

**Effective date:** 2026-04-25

## What Spendula is

Spendula is a single-user, self-hosted personal-finance tool. It imports the
operator's own bank transactions (via Enable Banking, a PSD2 Account
Information Service Provider) into the operator's own YNAB (You Need A Budget)
account, for the operator's personal budgeting use. It is not offered as a
service to any third party. Each deployment processes exclusively the bank
accounts of the natural person operating it.

## Who runs this instance

This Spendula instance is operated by:

- **Name:** Lucian Daniliuc
- **Country of residence:** Portugal
- **Contact for data-protection matters:** lucian@monitive.com

The operator is also the only data subject whose personal data is processed by
this instance. The operator runs the software on their own infrastructure
behind a private Tailscale network and is the sole controller of the data.

## What data is processed

When the operator authenticates a bank through Enable Banking, the following
categories of personal data flow into Spendula's local database under the
operator's PSD2 consent:

- Account identifiers (IBAN, BIC, account holder name)
- Account metadata (account type, currency, bank name, product name)
- Transaction details (amount, currency, value date, booking date, status,
  remittance information, counterparty name, counterparty IBAN where
  available, end-to-end identifier, structured creditor reference)
- The raw API response envelope from Enable Banking, retained for debugging
  and recovery

Spendula does not collect any data from anyone other than the operator, and
does not access or initiate payments — it uses Account Information Services
(AIS) only.

## Why it is processed (legal basis)

The lawful basis under the GDPR (Regulation (EU) 2016/679) is **explicit
consent** under Article 6(1)(a), given by the operator each time a bank
connection is authorised. PSD2 (Directive (EU) 2015/2366) requires that this
consent be granted directly to the AIS provider (Enable Banking) at the bank's
own consent screen.

The processing purpose is strictly the operator's personal budgeting and
record-keeping; the data is not used for any other purpose, profiling,
analytics, advertising, or training of any model.

## Where it is stored

Bank and transaction data live in a PostgreSQL database on infrastructure
controlled by the operator, reachable only over the operator's private
Tailscale network. The Enable Banking JWT-signing private key and the YNAB
personal access token are stored on the same host with restricted filesystem
permissions and are never transmitted off it except when calling the
respective APIs over TLS.

Backups, if any, are the operator's responsibility and stored on the
operator's own infrastructure.

## Who else sees it (sub-processors)

Spendula relies on two third-party services to perform its function:

- **Enable Banking Oy** — the regulated PSD2 AISP that fetches bank data on
  the operator's behalf. Their privacy policy:
  https://enablebanking.com/privacy-policy/
- **You Need A Budget LLC ("YNAB")** — the operator's chosen budgeting
  destination. Approved transactions are pushed to the operator's YNAB plan.
  Their privacy policy: https://www.ynab.com/privacy-policy

No other third parties receive any of the data. The repository is hosted on
GitHub, but no operator data is ever transmitted to GitHub — only source code.

## Retention

Data is retained on the operator's infrastructure for as long as the operator
wishes. There is no automatic retention limit. The operator can delete any or
all stored data at any time by dropping the relevant tables or removing the
host.

## Your rights

Because the operator is also the only data subject, the GDPR rights to access,
rectification, erasure, restriction, portability, and objection are exercised
by the operator directly on their own infrastructure.

If you are not the operator and you believe Spendula is processing data about
you, please contact the address below — by design, this should not be
possible, and any such occurrence is a defect.

## Security

- All API traffic uses TLS.
- The Enable Banking private key is bind-mounted read-only into the
  application container.
- The single HTTP endpoint exposed by the application (the OAuth callback)
  validates a CSRF state value and is reachable only over the operator's
  Tailscale network, fronted by Caddy with rate limiting.
- No login is exposed; there is no public web interface.

## Changes

If this policy changes, the **Effective date** above will be updated. Material
changes (new sub-processors, new categories of data processed, change of
operator) will be reflected here before the change takes effect.

## Contact

For any data-protection question or request:

**lucian@monitive.com**
