# Footer

To edit the footer on all the pages, search for `<footer class="app-footer">` in the `src/App/templates/layout/default.html.twig` template.
The content is usually basic `HTML` and `CSS` with `twig`.

Below is an example of a footer that groups urls under two categories and columns.
It also contains the copyright row.

```twig
<footer class="app-footer">
    <div class="container container-border">
        <div class="row">
            <div class="col-md-9">
                <div class="footer_head">
                    <h2>Category 1</h2>
                </div>
                <div class="row">
                    <div class="col-md-6 dk_widget">
                        <p class="footer-item-title">
                            Column 1
                        </p>
                        <p class="footer-item-link margin-small">
                            <a href="https://first.example.com/" target="_blank">
                                <img src="{{ asset('images/app/icon/hand.svg') }}">
                                First Link
                            </a>
                        </p>
                        <p class="footer-item-link margin-small">
                            <a href="https://second.example.com/" target="_blank">
                                <img src="{{ asset('images/app/icon/hand.svg') }}">
                                Second Link
                            </a>
                        </p>
                    </div>
                    <div class="col-md-6 dk_widget">
                        <p class="footer-item-title">
                            Column 2
                        </p>
                        <p class="footer-item-link margin-large">
                            <a href="https://third.example.com/" target="_blank">
                                <img src="{{ asset('images/app/icon/hand.svg') }}">
                                Third Link
                            </a>
                        </p>
                    </div>
                </div>
            </div>
            <div class="col-md-3">
                <div class="footer_head">
                    <h2>Category 2</h2>
                </div>
                <p class="footer-item-support margin-small">
                    <a href="https://fourth.example.com/" target="_blank">
                        <img src="{{ asset('images/app/icon/hand.svg') }}">
                        Fourth Link
                    </a>
                </p>
                <p class="footer-item-support margin-small">
                    <a href="https://fifth.example.com/" target="_blank">
                        <img src="{{ asset('images/app/icon/hand.svg') }}">
                        Fifth Link
                    </a>
                </p>
            </div>
        </div>

        <div class="row">
            <p class="footer-headline">
                © {{ 'now' | date('Y') }} by <a href="{{ url('home') }}">My Project</a>
            </p>
        </div>
    </div>
</footer>
```
