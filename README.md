# FHIR to Beacon deployment

Shows, by means of an example, how data from a BBMRI/GBA FHIR store can be uploaded to a local [Beacon 2.0 search API](http://docs.genomebeacons.org/) instance.

The deployment comprises of the following:

- Starting a FHIR store.
- Generating fake medical data and loading it to the FHIR store.
- Reading the data from the FHIR store and converting it to Beacon friendly format (BFF).
- Uploading the BFF data to a running Beacon API.
- Accessing the API via a browser.

This deployment is fully self-contained, but you will need to carry out a few tasks before it can be run.

## Setup

Create working directories:

```
mkdir bff images
```

Clone relevant repositories from GitHub:

```
cd images
git clone https://github.com/EGA-archive/beacon-2.x-training-ui.git
git clone https://github.com/EGA-archive/beacon2-ri-api.git
```

Create a local Beacon API image:

```
cd beacon2-ri-api
```

edit `deploy/conf.py` and change the `database_host` line to:

```
database_host = 'mongo'
```

Now build:

```
git build -t egarchive/beacon:2.0 . --no-cache
cd ../..
```

## Running

```
docker-compose up
```

Wait for the test data to finish loading (about three minutes). Then try this (in a different console):

```
curl http://localhost:5050/api/individuals/
curl http://localhost:5050/api/biosamples/
```

This should return lists of patients (individuals) and samples known to the store. Expect 2000 individuals and about ten times as many samples.

## License

Copyright 2023 The Samply Community
Licensed under the Apache License, Version 2.0 (the "License"); you may not use this file except in compliance with the License. You may obtain a copy of the License at
http://www.apache.org/licenses/LICENSE-2.0
Unless required by applicable law or agreed to in writing, software distributed under the License is distributed on an "AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied. See the License for the specific language governing permissions and limitations under the License.
