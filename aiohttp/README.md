### Data parameters

    json_data = await request.json()  # get POSTed json
    form_data = await request.post()  # get POSTed form data (`application/x-www-form-urlencoded` or `multipart/form-data`)
    name = request.query.get('name')  # get a query param value
    name = request.query.getall('name')  # get multiple query param values
