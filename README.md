# SharePoint-REST-API-Mail-
How to send mail using REST API in Sharepoint

// REST API For sending Mail using jquery/Javascript

$.ajax({
		url: _spPageContextInfo.webAbsoluteUrl + "/_api/Web/GetUserById(" + userid + ")",
		method: "GET",
		headers: { "Accept": "application/json; odata=verbose" },
		success: function (data) {
				var toAddress = "sample@sample.com";
				var fromAddress ="sample@sample.com";
				var ccAddress ="sample@sample.com";
				var emSubject = "Welcome!";
				var valMessage = "<div>Your Message</div>";
				var emBody = valMessage;

				var data = {
					properties: {
						__metadata: { 'type': 'SP.Utilities.EmailProperties' },
						From: fromAddress,
						To: { 'results': [toAddress] } ,
						CC: { 'results': [ccAddress] },
						Body: emBody,
						Subject: emSubject
					}            
				}

				var urlTemplate = _spPageContextInfo.webAbsoluteUrl + "/_api/SP.Utilities.Utility.SendEmail";

				$.ajax({
					contentType: 'application/json',
					url: urlTemplate,
					type: "POST",
					data: JSON.stringify(data),
					headers: {
						"Accept": "application/json;odata=verbose",
						"content-type": "application/json;odata=verbose",
						"X-RequestDigest": $("#__REQUESTDIGEST").val()
					},
					beforeSend: function(){ 
					},
					success: function (data) {
						alert("Mail Sent Sucessfully");
					},
					error: function (err) {

					}
				});
		},
		error: function (data,error) {
			//alert("Error : " +error);
		}
		});

