# Victor Yon Personal Website

Based on [al-folio](https://github.com/alshedivat/al-folio)

## Change content

- Resume: [`assets/json/resume.json`](assets/json/resume.json)
- Papers: [`_bibliography/papers.bib`](_bibliography/papers.bib)

## Local setup using Docker

- First, install [docker](https://docs.docker.com/get-docker/) and [docker-compose](https://docs.docker.com/compose/install/).
- Finally, run the following command that will pull the latest pre-built image from DockerHub and will run the website.

```bash
$ sudo docker compose pull
$ sudo docker compose up
```

Then open your browser and go to `http://localhost:8080`.
