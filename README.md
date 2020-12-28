# notes-frontend-tools

Notes made based on frontend master book:
https://frontendmasters.com/books/front-end-handbook/2019/#6.37

## Security:

### XSS(Cross site scripting)

#### Persistent XSS

XSS is basically enabled **when you allow the user to enter information, which you store (in your backend) and then present back**.

```
//Enter this as the input of a form and it will be saved to database
<script>alert('test')</script>
```

#### Reflected XSS

Reflected XSS is a way to exploit a vulnerability in your site on-the-fly by providing the end user a link that has a script inside it.

```
//Provide this link for victim to click it
yoursite.com/?example=<script>alert('test')</script>
```

#### DOM-based XSS



### Prevent XSS attacks

https://github.com/cure53/DOMPurify

https://jsxss.com/en/try.html

https://html5sec.org/

https://gist.github.com/kurobeats/9a613c9ab68914312cbb415134795b45

- encoding
- validation
- CSP

#### Encoding
```
//Before
<script>
//After
%3Cscript%3E
```

#### Validation

Whitelist or blacklist HTML tag, as encoding cannot be done (e.g. Wordpress allows users input html tag in Post directly)

#### CSP(Content security policy)

Can be done by client-side and server-side:

##### Client side

Use as a meta tag with `http-equiv`

P.S. `http-equiv` can only accept certains values: https://developer.mozilla.org/en-US/docs/Web/HTML/Element/meta

https://content-security-policy.com/examples/meta/

Starter Policy
This policy allows images, scripts, AJAX, form actions, and CSS from the same origin, and does not allow any other resources to load (eg object, frame, media, etc). It is a good starting point for many sites.

https://content-security-policy.com/#source_list

```
default-src 'none'; script-src 'self'; connect-src 'self'; img-src 'self'; style-src 'self';base-uri 'self';form-action 'self'
```

##### Server side

Use as HTTP header

https://content-security-policy.com/

The following points from here: https://konstantinlebedev.com/security-for-frontend/

#### X-XSS-Protection

Fallbacks for browser that doesn't support CSP, for example IE. (Default for modern browser, but good to have)

https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/X-XSS-Protection

#### Feature-Policy

Disable unused features

```
"Feature-Policy": "accelerometer 'none'; ambient-light-sensor 'none'; autoplay 'none'; camera 'none'; encrypted-media 'none'; fullscreen 'self'; geolocation 'none'; gyroscope 'none'; magnetometer 'none'; microphone 'none'; midi 'none'; payment 'none';  picture-in-picture 'none'; speaker 'none'; sync-xhr 'none'; usb 'none'; vr 'none';"
```

#### Referrer-Policy

Prevent any data from leaking when users navigates away from your website.

```
"Referrer-Policy": "no-referrer"
```

#### Subresource Integrity 

Use subresource integrity for checking if resources match

https://developer.mozilla.org/en-US/docs/Web/Security/Subresource_Integrity
