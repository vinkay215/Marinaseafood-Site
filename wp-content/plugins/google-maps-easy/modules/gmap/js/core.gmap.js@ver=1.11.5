var g_gmpLibJsLoaded = false;
function gmpLoadGoogleLib() {
	if(!g_gmpLibJsLoaded) {
		jQuery('head').append('<script src="'+ GMP_DATA.gmapApiUrl+ '"></script>');
		g_gmpLibJsLoaded = true;
	}
}
// Maps
function gmpGoogleMap(elementId, params, additionalData) {
	if(typeof(google) === 'undefined') {
		gmpLoadGoogleLib();
		//alert('Please check your Internet connection - we need it to load Google Maps Library from Google Server');
		//return false;
	}

	params = params ? params : {};
	additionalData = additionalData ? additionalData : {};
	var defaults = {
		center: new google.maps.LatLng(40.69847032728747, -73.9514422416687)
	,	zoom: 8
	//,	mapTypeId: google.maps.MapTypeId.ROADMAP
	};
	if(params.map_center && params.map_center.coord_x && params.map_center.coord_y) {
		params.center = new google.maps.LatLng(params.map_center.coord_x, params.map_center.coord_y);
	}
	if(params.zoom) {
		params.zoom = parseInt(params.zoom);
	}
	if(!GMP_DATA.isAdmin && params.zoom_type == 'zoom_level' && params.zoom_mobile && jQuery(document).width() < 768) {
		params.zoom = parseInt(params.zoom_mobile);
	}
	if (typeof(elementId) === 'string') {
		elementId = jQuery(elementId)[0];
	}
	this._elementId = elementId;
	this._mapParams = jQuery.extend({}, defaults, params);
	this._mapObj = null;
	this._markers = [];
	this._shapes = [];
	this._heatmap = [];
	this._clasterer = null;
	this._clastererEnabled = false;
	this._clastererMarkersGroupsStyles = [];
	this._eventListeners = {};
	this._layers = {};
	this.mapMarkersGroups = additionalData.markerGroups ? additionalData.markerGroups : [];
	this.init();
}
gmpGoogleMap.prototype.init = function() {
	this._beforeInit();
	this._mapObj = new google.maps.Map(this._elementId, this._mapParams);
	this._afterInit();
};
gmpGoogleMap.prototype._beforeInit = function() {
	if(typeof(this._mapParams.type_control) !== 'undefined') {
		if(typeof(google.maps.MapTypeControlStyle[ this._mapParams.type_control ]) !== 'undefined') {
			this._mapParams.mapTypeControlOptions = {
				style: google.maps.MapTypeControlStyle[ this._mapParams.type_control ]
			};
			this._mapParams.mapTypeControl = true;
		} else {
			this._mapParams.mapTypeControl = false;
		}
	}
	if(typeof(this._mapParams.zoom_control) !== 'undefined') {
		if(typeof(google.maps.ZoomControlStyle[ this._mapParams.zoom_control ]) !== 'undefined') {
			this._mapParams.zoomControlOptions = {
				style: google.maps.ZoomControlStyle[ this._mapParams.zoom_control ]
			};
			this._mapParams.zoomControl = true;
		} else {
			this._mapParams.zoomControl = false;
		}
	}
	if(typeof(this._mapParams.street_view_control) !== 'undefined') {
		this._mapParams.streetViewControl = parseInt(this._mapParams.street_view_control) ? true : false;
	}
	if(typeof(this._mapParams.pan_control) !== 'undefined') {
		this._mapParams.panControl = parseInt(this._mapParams.pan_control) ? true : false;
	}
	if(typeof(this._mapParams.overview_control) !== 'undefined') {
		if(this._mapParams.overview_control !== 'none') {
			this._mapParams.overviewMapControlOptions = {
				opened: this._mapParams.overview_control === 'opened' ? true : false
			};
			this._mapParams.overviewMapControl = true;
		} else {
			this._mapParams.overviewMapControl = false;
		}
	}
	if(typeof(this._mapParams.dbl_click_zoom) !== 'undefined') {
		this._mapParams.disableDoubleClickZoom = parseInt(this._mapParams.dbl_click_zoom) ? false : true;	// False/true in revert order - because option actually is for disabling this feature
	}
	if(typeof(this._mapParams.mouse_wheel_zoom) !== 'undefined') {
		this._mapParams.scrollwheel = parseInt(this._mapParams.mouse_wheel_zoom) ? true : false;
	}
	if(typeof(this._mapParams.map_type) !== 'undefined'
		&& typeof(google.maps.MapTypeId[ this._mapParams.map_type ]) !== 'undefined'
	) {
		this._mapParams.mapTypeId = google.maps.MapTypeId[ this._mapParams.map_type ];
	}
	if(typeof(this._mapParams.map_stylization_data) !== 'undefined'
		&& this._mapParams.map_stylization_data
	) {
		this._mapParams.styles = this._mapParams.map_stylization_data;
	}
	jQuery(document).trigger('gmapBeforeMapInit', this);
};
gmpGoogleMap.prototype.getParams = function(){
	return this._mapParams;
};
gmpGoogleMap.prototype.getParam = function(key){
	return this._mapParams[ key ];
};
gmpGoogleMap.prototype.setParam = function(key, value){
	this._mapParams[ key ] = value;
	return this;
};
gmpGoogleMap.prototype._afterInit = function() {
	if(typeof(this._mapParams.marker_clasterer) !== 'undefined' && this._mapParams.marker_clasterer) {
		this.enableClasterization(this._mapParams.marker_clasterer);
	}
	this.applyZoomType();
	if(typeof(this._mapParams.zoom_min) !== 'undefined' && typeof(this._mapParams.zoom_max) !== 'undefined') {
		this._setMinZoomLevel();
		this._setMaxZoomLevel();
		this._fixZoomLevel();
	}
	this.resizeMapByHeight();
	jQuery(window).bind('resize', jQuery.proxy(this.resizeMapByHeight, this));
	jQuery(window).bind('orientationchange', jQuery.proxy(this.resizeMapByHeight, this));
	jQuery(document).trigger('gmapAfterMapInit', this);
};
gmpGoogleMap.prototype._setMinZoomLevel = function() {
	var curZoom = this.getZoom();
	var minZoom = parseInt(this._mapParams.zoom_min) ? parseInt(this._mapParams.zoom_min) : null;
	this.getRawMapInstance().setOptions({minZoom: minZoom});
	if(curZoom < minZoom)
		this.getRawMapInstance().setOptions({zoom: minZoom});
};
gmpGoogleMap.prototype._setMaxZoomLevel = function() {
	var maxZoom = parseInt(this._mapParams.zoom_max) ? parseInt(this._mapParams.zoom_max) : null;
	this.getRawMapInstance().setOptions({maxZoom: maxZoom});
	if(this.getRawMapInstance().zoom > maxZoom)
		this.getRawMapInstance().setOptions({zoom: maxZoom});
};
gmpGoogleMap.prototype._fixZoomLevel = function() {
	var eventHandle = this._getEventListenerHandle('zoom_changed', 'zoomChanged');
	if(!eventHandle) {
		eventHandle = google.maps.event.addListener(this.getRawMapInstance(), 'zoom_changed', jQuery.proxy(function(){
			var minZoom = parseInt(this.getParam('zoom_min'))
			,	maxZoom = parseInt(this.getParam('zoom_max'));
			if (this.getZoom() < minZoom) {
				this.setZoom(minZoom);
				if(GMP_DATA.isAdmin && this._getEventListenerHandle('idle', 'enableClasterization'))
					google.maps.event.trigger(this.getRawMapInstance(), 'idle');
			}
			if (this.getZoom() > maxZoom) {
				this.setZoom(maxZoom);
				if(GMP_DATA.isAdmin && this._getEventListenerHandle('idle', 'enableClasterization'))
					google.maps.event.trigger(this.getRawMapInstance(), 'idle');
			}
		}, this));
		this._addEventListenerHandle('zoom_changed', 'zoomChanged', eventHandle);
	}
};
gmpGoogleMap.prototype.enableClasterization = function(clasterType, needTrigger) {
	needTrigger = needTrigger ? needTrigger : false;

	switch(clasterType) {
		case 'MarkerClusterer':	// Support only this one for now
			var self = this;

			self.setClastererMarkersGroupsStyles();

			var eventHandle = google.maps.event.addListenerOnce(self.getRawMapInstance(), 'idle', function(a, b, c){
				var clasterGridSize = self.getParam('marker_clasterer_grid_size')
				,	markerGroupsStyles = self.getClastererMarkersGroupsStyles();

				// Enable clasterization
				var allMapMarkers = self.getAllRawMarkers()
				,	allVisibleMapMarkers = []
				,	clasterer = self.getClasterer();

				for(var i = 0; i < allMapMarkers.length; i++) {
					if(allMapMarkers[i].getVisible() && !parseInt(allMapMarkers[i].params.clasterer_exclude)) {
						allVisibleMapMarkers.push(allMapMarkers[i]);
					}
				}
				if(clasterer){
					clasterer.clearMarkers();
					clasterer.addMarkers( allVisibleMapMarkers );
					clasterer.setStyles( markerGroupsStyles );

					self.setClastererGridSize(clasterGridSize);

					clasterer.resetViewport();
					clasterer.redraw();
				} else {
					clasterer = new MarkerClusterer(self.getRawMapInstance(), allVisibleMapMarkers, { styles: markerGroupsStyles, clusterClass: "cluster" });

					clasterer.setCalculator(self.customClastererCalculatorFunction( markerGroupsStyles ));
					self.setClasterer(clasterer);
					self.setClastererGridSize(clasterGridSize);

					clasterer = self.getClasterer();
				}
			});
			this._addEventListenerHandle('idle', 'enableClasterization', eventHandle);
			if(GMP_DATA.isAdmin || needTrigger) {
				google.maps.event.trigger(self.getRawMapInstance(), 'idle');
			}
			this._clastererEnabled = true;
			break;
	}
};
gmpGoogleMap.prototype.disableClasterization = function() {
	var eventHandle = this._getEventListenerHandle('idle', 'enableClasterization');
	if(eventHandle) {
		var clasterer = this.getClasterer();
		if(clasterer) {
			clasterer.clearMarkers();
			var markers = this.getAllRawMarkers();
			for(var i = 0; i < markers.length; i++) {
				markers[i].setMap( this.getRawMapInstance() );
			}
		}
		google.maps.event.removeListener( eventHandle );
		google.maps.event.trigger(this.getRawMapInstance(), 'idle');
		this._clastererEnabled = false;
	}
};
gmpGoogleMap.prototype.customClastererCalculatorFunction = function(markerGroupsStyles) {
	return function(markers, numStyles) {
		var styleIndex = 1, markersGroupsStyles = markerGroupsStyles, markersGroupsIds = {}, maxCount = 0, groupId = 0, curStyle = [];

		for (var i = 0; i < markers.length; i++) {
			if (markers[i].marker_group_id) {
				if (typeof(markersGroupsIds[markers[i].marker_group_id]) == 'undefined') {
					markersGroupsIds[markers[i].marker_group_id] = 1;
				} else {
					markersGroupsIds[markers[i].marker_group_id]++;
				}
			}
		}
		for (var currGroupId in markersGroupsIds) {
			if (markersGroupsIds[currGroupId] > maxCount) {
				maxCount = markersGroupsIds[currGroupId];
				groupId = currGroupId;
			}
		}
		curStyle = jQuery.grep(markersGroupsStyles, function (e, i) {
			if (e.marker_group_id == groupId) {
				return e;
			}
		});

		if (curStyle && curStyle[0])
			styleIndex = markersGroupsStyles.indexOf(curStyle[0]) + 1;

		return {
			text: markers.length,
			index: styleIndex
		};
	}
};
gmpGoogleMap.prototype.getClasterer = function() {
	if(this._clasterer) {
		return this._clasterer;
	}
	return false;
};
gmpGoogleMap.prototype.setClasterer = function(clasterer) {
	this._clasterer = clasterer;
};
gmpGoogleMap.prototype.setMapMarkersGroups = function(groups) {
	this.mapMarkersGroups = groups;
};
gmpGoogleMap.prototype.getMapMarkersGroups = function() {
	return this.mapMarkersGroups;
};
gmpGoogleMap.prototype.setClastererMarkersGroupsStyles = function() {
	var mapMarkersGroups = this.getMapMarkersGroups()
	,	markersGroupsStyles = this.getClastererMarkersGroupsStyles()
	,	defClasterIcon = GMP_DATA.modPath + 'gmap/img/m1.png'
	,	oldDefClasterIcon = 'https://google-maps-utility-library-v3.googlecode.com/svn/trunk/markerclusterer/images/m1.png'		// Prevent to use old default claster icon cdn icon because it is missing
	,	clasterIcon = this.getParam('marker_clasterer_icon')
	,	iconWidth = this.getParam('marker_clasterer_icon_width')
	,	iconHeight = this.getParam('marker_clasterer_icon_height');

	// Set claster base icon
	clasterIcon = clasterIcon && clasterIcon != oldDefClasterIcon ? clasterIcon : defClasterIcon;
	iconWidth = iconWidth ? iconWidth : 53;
	iconHeight = iconHeight ? iconHeight : 52;

	markersGroupsStyles.push({
		marker_group_id: 0
	,	url: clasterIcon
	,	width: iconWidth
	,	height: iconHeight
	});

	if(mapMarkersGroups) {
		for(var i = 0; i < mapMarkersGroups.length; i++) {
			var markerGroupId = mapMarkersGroups[i].id
			,	markerGroupClasterIcon = mapMarkersGroups[i].params.claster_icon
			,	markerGroupClasterIconWidth = mapMarkersGroups[i].params.claster_icon_width
			,	markerGroupClasterIconHeight = mapMarkersGroups[i].params.claster_icon_height;

			if(markerGroupClasterIcon && markerGroupClasterIcon != clasterIcon) {
				markersGroupsStyles.push({
					marker_group_id: markerGroupId
				,	url: markerGroupClasterIcon ? markerGroupClasterIcon : defClasterIcon
				,	width: markerGroupClasterIconWidth ? markerGroupClasterIconWidth : 53
				,	height: markerGroupClasterIconHeight ? markerGroupClasterIconHeight : 52
				, className: "cluster",
				});
			}
		}
	}
};
gmpGoogleMap.prototype.getClastererMarkersGroupsStyles = function() {
	return this._clastererMarkersGroupsStyles;
};
gmpGoogleMap.prototype.setClastererGridSize = function(size) {
	var clasterer = this.getClasterer();

	size = size && parseInt(size) ? parseInt(size) : null;

	if(clasterer && size) {
		clasterer.setGridSize(size);
	}
};
gmpGoogleMap.prototype.getClastererGridSize = function() {
	var clasterer = this.getClasterer()
		,	clusterGridSize = null;

	if(clasterer) {
		clusterGridSize =  clasterer.getGridSize();
	}
	return clusterGridSize;
};
/**
 * Should trigger after added or modified markers
 */
gmpGoogleMap.prototype.markersRefresh = function() {
	var clasterer = this.getClasterer();

	if(this._clastererEnabled && clasterer) {
		clasterer.clearMarkers();
		clasterer.addMarkers( this.getAllRawMarkers() );
	}
	jQuery(document).trigger('gmapAfterMarkersRefresh', this);
};
gmpGoogleMap.prototype._addEventListenerHandle = function(event, code, handle) {
	if(!this._eventListeners[ event ])
		this._eventListeners[ event ] = {};
	this._eventListeners[ event ][ code ] = handle;
};
gmpGoogleMap.prototype._getEventListenerHandle = function(event, code) {
	return this._eventListeners[ event ] && this._eventListeners[ event ][ code ]
		? this._eventListeners[ event ][ code ]
		: false;
};
gmpGoogleMap.prototype.getRawMapInstance = function() {
	return this._mapObj;
};
gmpGoogleMap.prototype.setCenter = function (lat, lng) {
	if(typeof lng == 'undefined'){
		this.getRawMapInstance().setCenter(lat);
	}else
		this.getRawMapInstance().setCenter(new google.maps.LatLng(lat, lng));
	return this;
};
gmpGoogleMap.prototype.getCenter = function () {
	return this.getRawMapInstance().getCenter();
};
gmpGoogleMap.prototype.setZoom = function (zoomLevel) {
	this.getRawMapInstance().setZoom(parseInt(zoomLevel));
};
gmpGoogleMap.prototype.getZoom = function () {
	return this.getRawMapInstance().getZoom();
};
gmpGoogleMap.prototype.getBounds = function () {
	return this.getRawMapInstance().getBounds();
};
gmpGoogleMap.prototype.fitBounds = function (bounds) {
	this.getRawMapInstance().fitBounds(bounds);
};
gmpGoogleMap.prototype.addMarker = function(params) {
	params.clusterClass = 'cluster';
	var newMarker = new gmpGoogleMarker(this, params);
	this._markers.push( newMarker );
	return newMarker;
};
gmpGoogleMap.prototype.addShape = function(params) {
	var newShape = new gmpGoogleShape(this, params);
	this._shapes.push( newShape );
	return newShape;
};
gmpGoogleMap.prototype.addHeatmap = function(params) {
	var heatmap = new gmpGoogleHeatmap(this, params);
	this._heatmap.push( heatmap );
	return heatmap;
};
gmpGoogleMap.prototype.getMarkerById = function(id) {
	if(this._markers && this._markers.length) {
		for(var i in this._markers) {
			if(this._markers[i].getId && this._markers[i].getId() == id)
				return this._markers[ i ];
		}
	}
	return false;
};
gmpGoogleMap.prototype.getShapeById = function(id) {
	if(this._shapes && this._shapes.length) {
		for(var i in this._shapes) {
			if(this._shapes[ i ].getId() == id)
				return this._shapes[ i ];
		}
	}
	return false;
};
gmpGoogleMap.prototype.getHeatmap = function() {
	if(this._heatmap && this._heatmap.length) {
		// There is only one heatmap layer on the map
		return this._heatmap[0];
	}
	return false;
};
gmpGoogleMap.prototype.removeMarker = function(id) {
	var marker = this.getMarkerById( id );
	if(marker) {
		marker.removeFromMap();
	}
};
gmpGoogleMap.prototype.removeShape = function(id) {
	var shape = this.getShapeById( id );

	if(shape) {
		shape.removeFromMap();
	}
};
gmpGoogleMap.prototype.getAllMarkers = function() {
	return this._markers;
};
gmpGoogleMap.prototype.getAllShapes = function() {
	return this._shapes;
};
/**
 * Retrive original Map marker objects (Marker objects from Google API)
 */
gmpGoogleMap.prototype.getAllRawMarkers = function() {
	var res = [];
	if(this._markers && this._markers.length) {
		for(var i = 0; i < this._markers.length; i++) {
			res.push( this._markers[i].getRawMarkerInstance() );
		}
	}
	return res;
};
gmpGoogleMap.prototype.setMarkersParams = function(markers) {
	if(this._markers && this._markers.length) {
		for(var i = 0; i < this._markers.length; i++) {
			for(var j = 0; j < markers.length; j++) {
				if(this._markers[i].getId() == markers[j].id) {
					this._markers[i].setMarkerParams( markers[j] );
					break;
				}
			}
		}
	}

};
gmpGoogleMap.prototype.get = function(key) {
	return this.getRawMapInstance().get( key );
};
// Set option for RAW MAP
gmpGoogleMap.prototype.set = function(key, value) {
	this.getRawMapInstance().set( key, value );
	return this;
};
gmpGoogleMap.prototype.clearMarkers = function() {
	if(this._markers && this._markers.length) {
		for(var i = 0; i < this._markers.length; i++) {
			this._markers[i].setMap( null );
		}
		this._markers = [];
	}
};
gmpGoogleMap.prototype.clearMarkersByParam = function(param) {
	if(this._markers && this._markers.length) {
		for(var i = 0; i < this._markers.length; i++) {
			if(this._markers[i].getMarkerParam(param)) {
				this._markers[i].setMap( null );
				this._markers.splice(i, 1);
				this.clearMarkersByParam(param);
				break;
			}
		}
	}
};
gmpGoogleMap.prototype.clearShapes = function() {
	if(this._shapes && this._shapes.length) {
		for(var i = 0; i < this._shapes.length; i++) {
			this._shapes[i].setMap( null );
		}
		this._shapes = [];
	}
};
gmpGoogleMap.prototype.getViewId = function() {
	return this._mapParams.view_id;
};
gmpGoogleMap.prototype.getViewHtmlId = function() {
	return this._mapParams.view_html_id;
};
gmpGoogleMap.prototype.getId = function() {
	return this._mapParams.id;
};
gmpGoogleMap.prototype.refresh = function() {
	return google.maps.event.trigger(this.getRawMapInstance(), 'resize');
};
gmpGoogleMap.prototype.refreshWithCenter = (function(lat, lng, zoom) {
	var res = google.maps.event.trigger(this.getRawMapInstance(), 'resize');
	if(zoom) {
		this.setZoom(zoom);
	} else {
		this.setZoom(this.getZoom());
	}
	if(lat && lng) {
		this.setCenter(lat, lng);
	} else {
		this.setCenter(this.getCenter().lat(), this.getCenter().lng());
	}
	return res;
});
gmpGoogleMap.prototype.fullRefresh = function() {
	this.refresh();
	this.checkMarkersParams(this._markers, false);
	this.setCenter( this._mapParams.center );
};
gmpGoogleMap.prototype.checkMarkersParams = function(markers, needToShow) {
	if(markers && markers.length) {
		for (var i = 0; i < markers.length; i++) {
			var markerParams = markers[i].getMarkerParam('params')
			,	showDescription = parseInt(markerParams.show_description);
			if(showDescription || needToShow) {
				markers[i].showInfoWnd( true, showDescription );
			}
		}
	}
};
gmpGoogleMap.prototype.resizeMapByHeight = function(e, elem, withoutAfter) {
	if(!GMP_DATA.isAdmin && parseInt(this.getParam('adapt_map_to_screen_height')) && this.getRawMapInstance().map_display_mode != 'popup') {
		var viewId = this.getParam('view_id')
		,	selectors = this.getParam('selectors')
		,	windowObj = jQuery(window)
		,	mapContainer = jQuery('#gmpMapDetailsContainer_' + viewId)
		,	mapContainerWrap = jQuery('#mapConElem_' + viewId)
		,	height;

		withoutAfter = withoutAfter ? withoutAfter : (mapContainerWrap.data('rmh-without-after') ? mapContainerWrap.data('rmh-without-after') : false);
		elem = elem ? elem : (mapContainerWrap.data('rmh-additional-elem') ? jQuery(mapContainerWrap.data('rmh-additional-elem')) : null);

		if(!selectors || (!selectors.content_before && !selectors.content_after)) {
			var mapContainerOffset = mapContainer.length ? mapContainer.offset() : false
			,	windowHeight = windowObj.height();
			height = mapContainerOffset.top < windowHeight ? windowHeight - mapContainerOffset.top : windowHeight;
		} else {
			var viewportData = this.getViewportData(0, withoutAfter)
			,	proControlsCon = jQuery('#gmpMapProControlsCon_'+ viewId);
			height = viewportData.height;
			mapContainer.parents('.gmp_map_opts:first').css({
				'position': 'fixed'
			,	'top': viewportData.contentBeforeHeight
			,	'left': '0'
			,	'width': windowObj.width()
			,	'height': height
			,	'z-index': 1
			});
			if(proControlsCon.find('.gmpMarkersListCollapseShell').length) {
				mapContainer.parents('.gmp_map_opts:first').css({
					'overflow-x': 'hidden'
				,	'overflow-y': 'auto'
				});
			}
			jQuery(selectors.content_before).css({
				'z-index': 2
			});
			if(!withoutAfter) {
				jQuery(selectors.content_after).css({
					'position': 'fixed'
				,	'bottom': '0'
				,	'left': '0'
				,	'width': windowObj.width()
				,	'z-index': 1
				});
			}
			if(elem && elem.length) {
				height -= elem.outerHeight(true);
			}
		}
		jQuery('#gmpMapDetailsContainer_' + viewId + ', #' + this.getParam('view_html_id')).each(function () {
			jQuery(this).height(height);
		});
		this.refresh();
	}
};
gmpGoogleMap.prototype.getViewportData = function(additionalHeight, withoutAfter) {
	withoutAfter = withoutAfter ? withoutAfter : false;
	additionalHeight = additionalHeight ? additionalHeight : 0;
	var selectors = this.getParam('selectors')
	,	adminBar = jQuery('#wpadminbar')	// fix for pages with admin bar
	,	viewportData = {
		height: jQuery(window).height(),
		contentBeforeHeight: 0,
		contentAfterHeight: 0
	}
	,	i;

	if(typeof selectors !== 'undefined' && selectors != null) {
		var contentBefore = typeof selectors.content_before !== 'undefined' ? jQuery(selectors.content_before) : 0
		,	contentAfter = typeof selectors.content_after !== 'undefined' ? jQuery(selectors.content_after) : 0;

		if(adminBar.length) {
			viewportData.contentBeforeHeight += adminBar.outerHeight(true);
		}
		if(contentBefore.length) {
			for(i = 0; i < contentBefore.length; i++) {
				viewportData.contentBeforeHeight += jQuery(contentBefore[i]).outerHeight(true);
			}
		}
		if(contentAfter.length && !withoutAfter) {
			for(i = 0; i < contentAfter.length; i++) {
				viewportData.contentAfterHeight += jQuery(contentAfter[i]).outerHeight(true);
			}
		}
	}
	viewportData.height = viewportData.height - viewportData.contentBeforeHeight - viewportData.contentAfterHeight - additionalHeight;
	return viewportData;
};
gmpGoogleMap.prototype.applyZoomType = function() {
	if(!GMP_DATA.isAdmin && this.getParam('zoom_type') == 'fit_bounds') {
		var eventHandle = google.maps.event.addListenerOnce(this.getRawMapInstance(), 'tilesloaded', jQuery.proxy(this._getBoundsHandler, this));
		this._addEventListenerHandle('tilesloaded', 'fitBounds', eventHandle);
	}
};
gmpGoogleMap.prototype.applyZoomTypeAdmin = function() {
	if(GMP_DATA.isAdmin && this.getParam('zoom_type') == 'fit_bounds') {
		// Call applyZoomTypeAdmin after refresh all map objects in admin area (markers, shapes, etc.)
		this._getBoundsHandler();
	}
};
// Free version of method
// see pro version here - google-maps-easy-pro/add_map_options/js/core.add_map_options.js
gmpGoogleMap.prototype._getBoundsHandler = function(){
	var bounds = new google.maps.LatLngBounds();

	bounds = this._getMapMarkersBounds(bounds);
	this._setMapBounds(bounds);
};
gmpGoogleMap.prototype._getMapMarkersBounds = function(bounds){
	var markers = this.getAllMarkers();

	for (var i = 0; i < markers.length; i++) {
		bounds.extend(markers[i].getPosition());
	}
	return bounds;
};
gmpGoogleMap.prototype._setMapBounds = function(bounds){
	// fit bounds only if map has more than one object
	if(!bounds.getNorthEast().equals(bounds.getSouthWest())) {
		this.fitBounds(bounds);
	}
};

// Common functions
var g_gmpGeocoder = null;
jQuery.fn.mapSearchAutocompleateGmp = function(params) {
	params = params || {};

    jQuery(this).keyup(function(event){
		// Ignore tab, enter, caps, end, home, arrows
		if(toeInArrayGmp(event.keyCode, [9, 13, 20, 35, 36, 37, 38, 39, 40])) return;

		var searchData = jQuery.trim(jQuery(this).val());

		if(searchData && searchData != '') {
			if(typeof(params.msgEl) === 'string') {
				params.msgEl = jQuery(params.msgEl);
			}
			params.msgEl.showLoaderGmp();
			var self = this;

			jQuery(this).autocomplete(jQuery.extend({}, params.autocompleteParams, {
				source: function(request, response) {
					var autocomleateData = typeof(params.additionalData) != 'undefined' ? gmpAutocomleateData(params.additionalData, request.term) : []
					,	geocoder = gmpGetGeocoder()
					,	geocoderData = { 'address': searchData };

					if(typeof(params.geocoderParams) != 'undefined' && params.geocoderParams) {
						geocoderData = jQuery.extend({}, geocoderData, params.geocoderParams)
					}
					geocoder.geocode(geocoderData, function(results, status) {
						params.msgEl.html('');

						if(status == google.maps.GeocoderStatus.OK && results.length) {
							for(var i = 0; i < results.length; i++) {
								autocomleateData.push({
									label: results[i].formatted_address
								,	lat: results[i].geometry.location.lat()
								,	lng: results[i].geometry.location.lng()
								,	category: toeLangGmp('Plases')
								});
							}
							response(autocomleateData);
						} else {
							if(autocomleateData) {
								response(autocomleateData);
							} else {
								//var notFoundMsg = toeLangGmp('Google can\'t find requested address coordinates, please try to modify search criterias.');
								var notFoundMsg = toeLangGmp('Nothing was found');

								if(jQuery(self).parent().find('.ui-helper-hidden-accessible').length) {
									jQuery(self).parent().find('.ui-helper-hidden-accessible').html(notFoundMsg);
								} else {
									params.msgEl.html(notFoundMsg);
								}
							}
						}
					});
				}
			,	select: function(event, ui) {
					if(params.onSelect) {
						params.onSelect(ui.item, event, ui);
					}
				}
			}));

			// Force imidiate search right after creation
			jQuery(this).autocomplete('search');
		}
	});
};
function gmpAutocomleateData(data, needle) {
	var autocomleateData = [];

	for(var i = 0; i < data.length; i++) {
		for(var j = 0; j < data[i].length; j++) {
			if(data[i][j]) {
				var label = data[i][j].label.toString().toLowerCase()
				,	desc = data[i][j].marker_desc != 'undefined' ? data[i][j].marker_desc : ''
				,	term = needle.toLowerCase();

				if(label.indexOf(term) !== -1 || (desc && desc.indexOf(term) !== -1)) {
					autocomleateData.push(data[i][j]);
				}
			}
		}
	}
	return autocomleateData;
}
function gmpGetGeocoder() {
	if(!g_gmpGeocoder) {
		g_gmpGeocoder = new google.maps.Geocoder();
	}
	return g_gmpGeocoder;
}
function changeInfoWndType(map) {

	//This is a standart google maps api class
	var infowndContent = jQuery('#'+ map._elementId.id).find('.gm-style-iw')
	,	type = map.getParam('marker_infownd_type')
	,	hideInfoWndBtn = parseInt(map.getParam('marker_infownd_hide_close_btn'));
	switch(type) {
		case '':
		if(infowndContent && infowndContent.length) {
			infowndContent.each(function() {
				var $this = jQuery(this)
				,	wndBody = $this.prev().children().last()
				,	wndBodyShadow = $this.prev().children(':nth-child(2)')
				,	wndTail = $this.prev().children(':nth-child(3)')
				,	wndTailShadow = $this.prev().children().first();
				$this.css({
					'border-radius': '0px'
				});
			});
		}
		break;
		case 'rounded_edges':
			if(infowndContent && infowndContent.length) {
				infowndContent.each(function() {
					var $this = jQuery(this)
					,	wndBody = $this.prev().children().last()
					,	wndBodyShadow = $this.prev().children(':nth-child(2)')
					,	wndTail = $this.prev().children(':nth-child(3)')
					,	wndTailShadow = $this.prev().children().first();

					if(hideInfoWndBtn !== 0) {
						//$this.next('div').hide();
						$this.find(".gm-ui-hover-effect").hide();
					}
					$this.find('.gmpInfoWindowtitle').css({
						'padding': '0'
					,	'left': '0'
					});
					wndBody.css({
						'border-radius': '10px'
					});
					wndBodyShadow.css({
						'background-color': 'transparent',
						'-moz-box-shadow': 'none',
						'-webkit-box-shadow': 'none',
						'box-shadow': 'none'
					});
					wndTail.children().each(function(index) {
						var $this = jQuery(this)
						,	degrees = !index ? 'skewX(50.6deg)' : 'skewX(-50.6deg)'
						,	left = !index ? '-2px' : '0';

						$this.css({
							'height': '15px'
						});
						$this.children().css({
							'width': '20px'
						,	'left': left
						,	'transform': degrees
						,	'-moz-box-shadow': 'none'
						,	'-webkit-box-shadow': 'none'
						,	'box-shadow': 'none'
						});
					});
					wndTailShadow.css({
						'border-right': 'none'
					,	'border-left': 'none'
					,	'border-top': 'none'
					,	'left': '38px'
					,	'top': '74px'
					});
				});
			}
			break;
		default:
			break;
	}
}
function changeInfoWndBgColor(map) {
	g_gmpMarkerBgColorTimeoutSet = false;
	var color = map.getParam('marker_infownd_bg_color');

	//This is a standart google maps api class
	var infowndContent = jQuery('#'+ map._elementId.id).find('.gm-style-iw'),
		styleId = 'gmpInfoWindowStyle';

	if(infowndContent && infowndContent.length) {
		infowndContent.each(function() {
			var wndBody = jQuery(this).prev().children().last()
			,	wndTail = jQuery(this).prev().children(':nth-child(3)').children().last();
			//wndBody.css('background-color', color);
			//wndTail.prev().children().last().css('background-color', color);
			//wndTail.children().css('background-color', color);
			infowndContent.css('background-color', color);
			infowndContent.prev().children().last().css('background-color', color);
			infowndContent.children().css('background-color', color);
			var styleTag = jQuery('#'+styleId),
				styles = '.gm-style-iw-t::after { background:'+color+' !important; }';

			styles += '.gm-style .gm-style-iw-d::-webkit-scrollbar-track, .gm-style .gm-style-iw-d::-webkit-scrollbar-track-piece { background: '+color+' !important; }';
			if(styleTag.length) {
				styleTag.html(styles);
			} else {
				jQuery('<style>'+styles+'</style>').attr('id', styleId).appendTo('head');
			}
		});
	}
}

window.gmpGoogleMap = gmpGoogleMap;
