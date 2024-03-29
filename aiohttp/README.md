### Request data

    json_data = await request.json()  # get POSTed json
    form_data = await request.post()  # get POSTed form data (`application/x-www-form-urlencoded` or `multipart/form-data`)
    name = request.query.get('name')  # get a query param value
    name = request.query.getall('name')  # get multiple query param values


### Responses

    text_content = "Hello, World!"
    web.Response(text=text_content)

    html_content = "<html><body><h1>Hello, World!</h1></body></html>"
    web.Response(text=html_content, content_type='text/html')

    data = {"message": "Hello, World!"}
    web.json_response(data)

    web.Response(text="404: Content Not Found", status=404)

    data = {"error": "Resource not found"}
    web.json_response(data, status=404)

    web.Response(text="Forbidden", status=403, content_type='text/plain')

    response = web.HTTPFound(location='/')
    raise response

    web.Response(status=200, headers={'HX-Redirect': new_location})
