Routes
------

A ``Route`` aggregate all the main entities, the generic parameters are:

    * ``provider``: a provider instance
    * ``message_translator``: a message translator instance
    * ``handler``: a handler instance
    * ``error_handler`` (optional): an error handler instance
    * ``name`` (optional): a name for this route


We provide some helper routes, so you don't need to setup all this boilerplate code:

    * ``loafer.ext.aws.routes.SQSRoute``: a route that configures a
      ``loafer.ext.aws.providers.SQSProvider`` and
      ``loafer.ext.aws.message_translators.SQSMessageTranslator``.
      A route for handlers that consume messages from SQS queue (expects json format messages).

    * ``loafer.ext.aws.routes.SNSQueueRoute``: a route that configures a
      ``loafer.ext.aws.providers.SQSProvider`` and
      ``loafer.ext.aws.message_translators.SNSMessageTranslator``.
      A route for handlers that consume messages from a SQS queue subscribed to
      a SNS topic (expects json format messages).


Examples
~~~~~~~~

Some examples of route creation::

    from loafer.ext.aws.routes import SQSRoute, SNSQueueRoute

    # regular route
    route1 = SQSRoute('my-queue1', handler=..., name='route1')

    # route with custom SQSProvider parameters
    route2 = SNSQueueRoute('my-queue2', {'use_ssl': False, 'options': {'WaitTimeSeconds': 4}}, handler=..., name='route2')

    # route with custom message translator
    route3 = SQSRoute('my-queue3', message_translator=custom_message_translator, handler=...)

    # route with custom error handler
    route4 = SNSQueueRoute('my-queue4', handler=..., error_handler=custom_error_handler)