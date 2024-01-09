# Laravel Blade Templating Engine

## Master layout setup and some features
- One can create a separate file for a layout and use it later for a page in order to reuse the code and not repeating it always.
- Using the template engine, you can create sections which has a `yield` keyword on the layout file.
- One can use PHP's built-in functions as long as it is enclosed inside the curly brackets `{{` and `}}`, e.g
```php
@section('content')

    <h1>Contact Page</h1>

    @if (count($people))
        <h2>People count: {{ count($people) }}</h2>
        <ul>
        @foreach($people as $person)
            <li>{{ $person }}</li>
        @endforeach
        </ul>
    @endif

@stop
```
