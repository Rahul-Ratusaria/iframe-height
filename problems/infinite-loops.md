# Infinite loops

As raised by [Jake Archibald](https://lists.w3.org/Archives/Public/www-style/2016Feb/0065.html), this could "suffer from the same infinite loop issue as element queries".

It is possible that the framed content includes a media query that is based on **height**, and this is a problem, as unlike a normal viewport, this **height** is now dependent on the content.

But we *can* cheat here, as we don't need to consider every edge case that the "element queries" proposal needed to consider.

We just need to let the browser do an initial layout, and if it determines a second pass is necessary, then **lock** the height, and use scroll bars as we do today.

---

In most cases this won't be a problem, as the `iframe` only needed to change the **height**, whereas most media queries are based on the **width**.

This is because the **width** is being enforced by the viewport onto the content (as we hate horizontal scroll bars). Whereas the **height** is determined by the content, and is passed up from the content to the viewport (resulting in the vertical scroll bar).

And it's not like the current JavaScript solutions/hacks don't suffer from this problem.

---

For reference, this problem has already been addressed by:

* [Safari](https://lists.w3.org/Archives/Public/www-style/2016Feb/0187.html): Where Simon Fraser explained that they already use this for "frame flattening" on iOS.

* [FireFox](https://lists.w3.org/Archives/Public/www-style/2016Feb/0067.html): Where Robert O'Callahan implemented this for the seamless attribute.

The only opposition has been from [Ojan Vafai](https://lists.w3.org/Archives/Public/www-style/2016Feb/0180.html) (Chrome), who wants to half implement this feature via [ResizeObserver](https://lists.w3.org/Archives/Public/www-style/2016Feb/0252.html).
