### Properly specify `application/json`

    # GOOD
    $.ajax({
        url: path,
        type: 'POST',
        data: JSON.stringify(payload),
        contentType: 'application/json',
    });                                                        
                                                           
    # BAD -- jquery will url encode the payload! 
    $.ajax({
        url: path,
        type: 'POST',
        data: JSON.stringify(payload),
        headers: { 'Content-Type': 'application/json' },
    });  
