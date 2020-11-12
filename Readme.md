## pyramid-realworld-example-app


### Steps
1. Copy "" to src
2. Enable  pinpoint middleware 

``` python 

def main(global_config: t.Dict[str, str], **settings: str) -> Router:
    """Return a Pyramid WSGI application."""

    # Expand environment variables in .ini files
    settings = expandvars_dict(settings)

    # Configure Pyramid
    # TODO: can we configure root_factory in auth.py?
    # config.set_root_factory(root_factory) maybe?
    config = Configurator(settings=settings, root_factory="conduit.auth.RootFactory")
    config.add_tween('pinpoint.pyramid.tween.pinpoint_tween')       <---------------- pinpoint-middleware
    configure(config)

    # Up, Up and Away!
    return config.make_wsgi_app()

```