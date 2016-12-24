Links
^^^^^
Links are used to define one-to-many relationships between Assets and other Assets, between Assets and Streams, and between Assets and Spans.

Link types must define a single Source attribute, and N Target attributes, where the source attribute represents the index of an asset element, and the target attributes represent either the indices of other asset elements or span objects, or stream IDs of associated value streams. Each Source and Target attribute must include a ``linkType`` keyword which describes the type to be linked to or from, and optionally a ``linkTypeVersion`` keyword, which denotes the version of the ``linkType`` to use.

On-premises PI systems interpret a link object by building child AF elements beneath the Source element for each target Asset attribute, Event Frames for each target Span attribute, and PI data references for each target Value stream attribute.

AF elements can be built at the root level by sending a root link element with the Source attribute set to "_ROOT" and a Target attribute for each asset to be built at the root level.

Child elements, Event Frames, and data references cannot be built until the parent asset has been built, either via a root link, or a chain of links that resolve up to a root link.

Links are not presently supported in cloud-based systems.
