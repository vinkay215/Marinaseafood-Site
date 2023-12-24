if(typeof(GMP_DATA) == 'undefined')
	var GMP_DATA = {};
if(isNumber(GMP_DATA.animationSpeed))
    GMP_DATA.animationSpeed = parseInt(GMP_DATA.animationSpeed);
else if(jQuery.inArray(GMP_DATA.animationSpeed, ['fast', 'slow']) == -1)
    GMP_DATA.animationSpeed = 'fast';
GMP_DATA.showSubscreenOnCenter = parseInt(GMP_DATA.showSubscreenOnCenter);
var sdLoaderImgGmp = '<img src="'+ GMP_DATA.loader+ '" />';
var g_gmpAnimationSpeed = 300;

jQuery.fn.showLoaderGmp = function() {
    return jQuery(this).html( sdLoaderImgGmp );
};
jQuery.fn.appendLoaderGmp = function() {
    jQuery(this).append( sdLoaderImgGmp );
};
jQuery.sendFormGmp = function(params) {
	// Any html element can be used here
	return jQuery('<br />').sendFormGmp(params);
};
/**
 * Send form or just data to server by ajax and route response
 * @param string params.fid form element ID, if empty - current element will be used
 * @param string params.msgElID element ID to store result messages, if empty - element with ID "msg" will be used. Can be "noMessages" to not use this feature
 * @param function params.onSuccess funstion to do after success receive response. Be advised - "success" means that ajax response will be success
 * @param array params.data data to send if You don't want to send Your form data, will be set instead of all form data
 * @param array params.appendData data to append to sending request. In contrast to params.data will not erase form data
 * @param string params.inputsWraper element ID for inputs wraper, will be used if it is not a form
 * @param string params.clearMsg clear msg element after receive data, if is number - will use it to set time for clearing, else - if true - will clear msg element after 5 seconds
 */
jQuery.fn.sendFormGmp = function(params) {
    var form = null;
    if(!params)
        params = {fid: false, msgElID: false, onSuccess: false};

    if(params.fid)
        form = jQuery('#'+ fid);
    else
        form = jQuery(this);

    /* This method can be used not only from form data sending, it can be used just to send some data and fill in response msg or errors*/
    var sentFromForm = (jQuery(form).tagName() == 'FORM');
    var data = new Array();
    if(params.data)
        data = params.data;
    else if(sentFromForm)
        data = jQuery(form).serialize();

    if(params.appendData) {
		var dataIsString = typeof(data) == 'string';
		var addStrData = [];
        for(var i in params.appendData) {
			if(dataIsString) {
				if(toeInArray(typeof(params.appendData[i], ['object', 'array']))) {
					for(var j in params.appendData[i]) {
						addStrData.push(i+ '['+ j+ ']'+ '='+ params.appendData[i][j]);
					}
				} else {
					addStrData.push(i+ '='+ params.appendData[i]);
				}

			} else
				data[i] = params.appendData[i];
        }
		if(dataIsString)
			data += '&'+ addStrData.join('&');
    }
    var msgEl = null;
    if(params.msgElID) {
        if(params.msgElID == 'noMessages')
            msgEl = false;
        else if(typeof(params.msgElID) == 'object')
           msgEl = params.msgElID;
       else
            msgEl = jQuery('#'+ params.msgElID);
    }
	if(typeof(params.inputsWraper) == 'string') {
		form = jQuery('#'+ params.inputsWraper);
		sentFromForm = true;
	}
	if(sentFromForm && form) {
        jQuery(form).find('*').removeClass('gmpInputError');
    }
	if(msgEl && !params.btn) {
		jQuery(msgEl).removeClass('gmpSuccessMsg')
			.removeClass('gmpErrorMsg')
			.showLoaderGmp();
	}
	if(params.btn) {
		jQuery(params.btn).attr('disabled', 'disabled');
		// Font awesome usage
		params.btnIconElement = jQuery(params.btn).find('.fa').length ? jQuery(params.btn).find('.fa') : jQuery(params.btn);
		if(jQuery(params.btn).find('.fa').length) {
			params.btnIconElement
				.data('prev-class', params.btnIconElement.attr('class'))
				.attr('class', 'fa fa-spinner fa-spin');
		}
	}
    var url = '';
	if(typeof(params.url) != 'undefined')
		url = params.url;
    else if(typeof(ajaxurl) == 'undefined')
        url = GMP_DATA.ajaxurl;
    else
        url = ajaxurl;

    jQuery('.gmpErrorForField').hide(GMP_DATA.animationSpeed);
	var dataType = params.dataType ? params.dataType : 'json';
	// Set plugin orientation
	if(typeof(data) == 'string') {
		data += '&pl='+ GMP_DATA.GMP_CODE;
		data += '&reqType=ajax';
	} else {
		data['pl'] = GMP_DATA.GMP_CODE;
		data['reqType'] = 'ajax';
	}

    jQuery.ajax({
        url: url,
        data: data,
        type: 'POST',
        dataType: dataType,
        success: function(res) {
            toeProcessAjaxResponseGmp(res, msgEl, form, sentFromForm, params);
			if(params.clearMsg) {
				setTimeout(function(){
					if(msgEl)
						jQuery(msgEl).animateClear();
				}, typeof(params.clearMsg) == 'boolean' ? 5000 : params.clearMsg);
			}
        }
    });
};
/**
 * Hide content in element and then clear it
 */
jQuery.fn.animateClear = function() {
	var newContent = jQuery('<span>'+ jQuery(this).html()+ '</span>');
	jQuery(this).html( newContent );
	jQuery(newContent).hide(GMP_DATA.animationSpeed, function(){
		jQuery(newContent).remove();
	});
};
/**
 * Hide content in element and then remove it
 */
jQuery.fn.animateRemoveGmp = function(animationSpeed, onSuccess) {
	animationSpeed = animationSpeed == undefined ? GMP_DATA.animationSpeed : animationSpeed;
	jQuery(this).hide(animationSpeed, function(){
		jQuery(this).remove();
		if(typeof(onSuccess) === 'function')
			onSuccess();
	});
};
function toeProcessAjaxResponseGmp(res, msgEl, form, sentFromForm, params) {
    if(typeof(params) == 'undefined')
        params = {};
    if(typeof(msgEl) == 'string')
        msgEl = jQuery('#'+ msgEl);
    if(msgEl)
        jQuery(msgEl).html('');
	if(params.btn) {
		jQuery(params.btn).removeAttr('disabled');
		if(params.btnIconElement) {
			params.btnIconElement.attr('class', params.btnIconElement.data('prev-class'));
		}
	}
    /*if(sentFromForm) {
        jQuery(form).find('*').removeClass('gmpInputError');
    }*/
    if(typeof(res) == 'object') {
        if(res.error) {
            if(msgEl) {
                jQuery(msgEl).removeClass('gmpSuccessMsg')
					.addClass('gmpErrorMsg');
            }
			var errorsArr = [];
            for(var name in res.errors) {
                if(sentFromForm) {
					var inputError = jQuery(form).find('[name*="'+ name+ '"]');
                    inputError.addClass('gmpInputError');
					if(inputError.attr('placeholder')) {
						//inputError.attr('placeholder', res.errors[ name ]);
					}
					if(!inputError.data('keyup-error-remove-binded')) {
						inputError.keydown(function(){
							jQuery(this).removeClass('gmpInputError');
						}).data('keyup-error-remove-binded', 1);
					}
                }
                if(jQuery('.gmpErrorForField.toe_'+ nameToClassId(name)+ '').exists())
                    jQuery('.gmpErrorForField.toe_'+ nameToClassId(name)+ '').show().html(res.errors[name]);
                else if(msgEl)
                    jQuery(msgEl).append(res.errors[name]).append('<br />');
				else
					errorsArr.push( res.errors[name] );
            }
			if(errorsArr.length && params.btn) {
				jQuery('<div />').html( errorsArr.join('<br />') ).appendTo('body').dialog({
					modal: true
				,	width: '500px'
				});
			}
        } else if(res.messages.length) {
            if(msgEl) {
                jQuery(msgEl).removeClass('gmpErrorMsg')
					.addClass('gmpSuccessMsg');
                for(var i = 0; i < res.messages.length; i++) {
                    jQuery(msgEl).append(res.messages[i]).append('<br />');
                }
            }
        }
    }
    if(params.onSuccess && typeof(params.onSuccess) == 'function') {
        params.onSuccess(res);
    }
}

function getDialogElementGmp() {
	return jQuery('<div/>').appendTo(jQuery('body'));
}

function toeOptionGmp(key) {
	if(GMP_DATA.options && GMP_DATA.options[ key ] && GMP_DATA.options[ key ].value)
		return GMP_DATA.options[ key ].value;
	return false;
}
function toeLangGmp(key) {
	if(GMP_DATA.siteLang && GMP_DATA.siteLang[key])
		return GMP_DATA.siteLang[key];
	return key;
}
function toePagesGmp(key) {
	if(typeof(GMP_DATA) != 'undefined' && GMP_DATA[key])
		return GMP_DATA[key];
	return false;;
}
/**
 * This function will help us not to hide desc right now, but wait - maybe user will want to select some text or click on some link in it.
 */
function toeOptTimeoutHideDescriptionGmp() {
	jQuery('#gmpOptDescription').removeAttr('toeFixTip');
	setTimeout(function(){
		if(!jQuery('#gmpOptDescription').attr('toeFixTip'))
			toeOptHideDescriptionGmp();
	}, 500);
}
/**
 * Show description for options
 */
function toeOptShowDescriptionGmp(description, x, y, moveToLeft) {
    if(typeof(description) != 'undefined' && description != '') {
        if(!jQuery('#gmpOptDescription').length) {
            jQuery('body').append('<div id="gmpOptDescription"></div>');
        }
		if(moveToLeft)
			jQuery('#gmpOptDescription').css('right', jQuery(window).width() - (x - 10));	// Show it on left side of target
		else
			jQuery('#gmpOptDescription').css('left', x + 10);
        jQuery('#gmpOptDescription').css('top', y);
        jQuery('#gmpOptDescription').show(200);
        jQuery('#gmpOptDescription').html(description);
    }
}
/**
 * Hide description for options
 */
function toeOptHideDescriptionGmp() {
	jQuery('#gmpOptDescription').removeAttr('toeFixTip');
    jQuery('#gmpOptDescription').hide(200);
}
function toeInArrayGmp(needle, haystack) {
	if(haystack) {
		for(var i in haystack) {
			if(haystack[i] == needle)
				return true;
		}
	}
	return false;
}
function toeShowDialogCustomized(element, options) {
	options = jQuery.extend({
		resizable: false
	,	width: 500
	,	height: 300
	,	closeOnEscape: true
	,	open: function(event, ui) {
			jQuery('.ui-dialog-titlebar').css({
				'background-color': '#222222'
			,	'background-image': 'none'
			,	'border': 'none'
			,	'margin': '0'
			,	'padding': '0'
			,	'border-radius': '0'
			,	'color': '#CFCFCF'
			,	'height': '27px'
			});
			jQuery('.ui-dialog-titlebar-close').css({
				'background': 'url("'+ GMP_DATA.cssPath+ 'img/tb-close.png") no-repeat scroll 0 0 transparent'
			,	'border': '0'
			,	'width': '15px'
			,	'height': '15px'
			,	'padding': '0'
			,	'border-radius': '0'
			,	'margin': '7px 7px 0'
			}).html('');
			jQuery('.ui-dialog').css({
				'border-radius': '3px'
			,	'background-color': '#FFFFFF'
			,	'background-image': 'none'
			,	'padding': '1px'
			,	'z-index': '300000'
			,	'position': 'fixed'
			,	'top': '60px'
			});
			jQuery('.ui-dialog-buttonpane').css({
				'background-color': '#FFFFFF'
			});
			jQuery('.ui-dialog-title').css({
				'color': '#CFCFCF'
			,	'font': '12px sans-serif'
			,	'padding': '6px 10px 0'
			});
			if(options.openCallback && typeof(options.openCallback) == 'function') {
				options.openCallback(event, ui);
			}
			jQuery('.ui-widget-overlay').css({
				'z-index': jQuery( event.target ).parents('.ui-dialog:first').css('z-index') - 1
			,	'background-image': 'none'
			});
			if(options.modal && options.closeOnBg) {
				jQuery('.ui-widget-overlay').unbind('click').bind('click', function() {
					jQuery( element ).dialog('close');
				});
			}
		}
	}, options);
	return jQuery(element).dialog(options);
}
/**
 * @see html::slider();
 **/
function toeSliderMove(event, ui) {
    var id = jQuery(event.target).attr('id');
	var unit = jQuery(event.target).parent().find('[data-unit]').attr('data-unit');
	if(ui.value == 1) {
		jQuery('#toeSliderDisplay_'+ id).html( ui.value + ' ' + unit );
	} else {
		jQuery('#toeSliderDisplay_'+ id).html( ui.value + ' ' + unit + 's' );
	}

    jQuery('#toeSliderInput_'+ id).val( ui.value ).change();
}
function setBrowserUrl(url) {
	if (typeof (history.pushState) != 'undefined') {
        var obj = {Title: document.title, Url: url};
        history.pushState(obj, obj.Title, obj.Url);
    }
}
function createAjaxLinkGmp(param) {
	return GMP_DATA.ajaxurl+ '?'+ paramGmp(param);
}
function paramGmp(param) {
	var param = jQuery.extend({}, param);
	param['pl'] = GMP_DATA.GMP_CODE;
	return jQuery.param( param );
}
/* TinyMCE Editor */
function gmpGetTxtEditorVal(id) {
	var elem = jQuery('#'+ id)
	,	content = typeof(tinyMCE) !== 'undefined' && tinyMCE.get( id ) && !elem.is(':visible')
			? tinyMCE.get( id ).getContent()
			: elem.val();
	return content;
}
function gmpSetTxtEditorVal(id, content) {
	var elem = jQuery('#'+ id);

	if(typeof(tinyMCE) !== 'undefined' && tinyMCE && tinyMCE.get( id ) && !elem.is(':visible')) {
		tinyMCE.get( id ).setContent(content);
	} else {
		elem.val( content );
	}

}
