# champ383

lesssgooo

1. JavaScript Code (afAgentforceFollowUpActions.js)
Properties to Add:
// Add these @track properties
@track showFeedbackModal = false;
@track feedbackOptions = [
    { label: 'Inaccurate', value: 'inaccurate', checked: false },
    { label: 'Incomplete', value: 'incomplete', checked: false },
    { label: 'Biased, toxic, or harmful', value: 'biased', checked: false },
    { label: 'Inappropriate tone or style', value: 'inappropriate', checked: false },
    { label: 'Other', value: 'other', checked: false }
];
@track feedbackText = '';
@track currentActionId = '';
Methods to Add:
// Thumbs Up Handler - Show success message
handleThumbsUp(event) {
    const actionId = event.target.dataset.actionId;
    
    this.dispatchEvent(
        new ShowToastEvent({
            title: 'Thanks for your feedback.',
            message: '',
            variant: 'success'
        })
    );
}

// Thumbs Down Handler - Show feedback modal
handleThumbsDown(event) {
    this.currentActionId = event.target.dataset.actionId;
    this.showFeedbackModal = true;
    this.resetFeedbackForm();
}

// Reset feedback form
resetFeedbackForm() {
    this.feedbackOptions = this.feedbackOptions.map(option => ({
        ...option,
        checked: false
    }));
    this.feedbackText = '';
}

// Handle checkbox changes in feedback modal
handleFeedbackOptionChange(event) {
    const value = event.target.value;
    this.feedbackOptions = this.feedbackOptions.map(option => ({
        ...option,
        checked: option.value === value ? event.target.checked : option.checked
    }));
}

// Handle feedback text change
handleFeedbackTextChange(event) {
    this.feedbackText = event.target.value;
}

// Submit feedback
handleSubmitFeedback() {
    const selectedOptions = this.feedbackOptions
        .filter(option => option.checked)
        .map(option => option.label);
    
    // Here you would typically send the feedback to your backend
    console.log('Feedback submitted:', {
        actionId: this.currentActionId,
        selectedOptions: selectedOptions,
        feedbackText: this.feedbackText
    });

    // Show success message
    this.dispatchEvent(
        new ShowToastEvent({
            title: 'Your response helps us to improve the model\'s performance and the user experience',
            message: '',
            variant: 'info'
        })
    );

    // Close modal
    this.closeFeedbackModal();
}

// Cancel feedback
handleCancelFeedback() {
    this.closeFeedbackModal();
}

// Close feedback modal
closeFeedbackModal() {
    this.showFeedbackModal = false;
    this.currentActionId = '';
    this.resetFeedbackForm();
}
2. HTML Code (afAgentforceFollowUpActions.html)
Thumbs Buttons Container:
<!-- RIGHT part (thumbs area) -->
<div class="thumbs-container">
    <lightning-button-icon
        icon-name="utility:like"
        alternative-text="Thumbs Up"
        title="Thumbs Up"
        variant="bare"
        data-action-id={ar.action.Id}
        onclick={handleThumbsUp}
        class="thumb-btn thumb-up">
    </lightning-button-icon>
    <lightning-button-icon
        icon-name="utility:dislike"
        alternative-text="Thumbs Down"
        title="Thumbs Down"
        variant="bare"
        data-action-id={ar.action.Id}
        onclick={handleThumbsDown}
        class="thumb-btn thumb-down">
    </lightning-button-icon>
</div>
Feedback Popover:
<!-- Feedback Popover -->
<template if:true={showFeedbackModal}>
    <div class="feedback-popover slds-popover slds-popover_medium slds-nubbin_bottom-right">
        <div class="slds-popover__header">
            <h3 class="slds-popover__title">
                Why wasn't it helpful?
                <lightning-icon
                    icon-name="utility:info"
                    alternative-text="Your response helps us to improve the model's performance and the user experience"
                    title="Your response helps us to improve the model's performance and the user experience"
                    size="x-small"
                    class="slds-m-left_x-small">
                </lightning-icon>
                <lightning-button-icon
                    icon-name="utility:close"
                    onclick={handleCancelFeedback}
                    alternative-text="close"
                    variant="bare"
                    size="x-small"
                    class="slds-m-left_x-small">
                </lightning-button-icon>
            </h3>
        </div>
        <div class="slds-popover__body">
            <div class="slds-form-element">
                <fieldset class="slds-form-element">
                    <legend class="slds-form-element__legend slds-form-element__label">Select all that apply: <span class="slds-required">*</span></legend>
                    <div class="slds-form-element__control">
                        <template for:each={feedbackOptions} for:item="option">
                            <div key={option.value} class="slds-checkbox slds-m-bottom_small">
                                <input 
                                    type="checkbox" 
                                    name="feedback-options"
                                    id={option.value}
                                    value={option.value}
                                    checked={option.checked}
                                    onchange={handleFeedbackOptionChange} />
                                <label class="slds-checkbox__label" for={option.value}>
                                    <span class="slds-checkbox__faux"></span>
                                    <span class="slds-form-element__label">{option.label}</span>
                                </label>
                            </div>
                        </template>
                    </div>
                </fieldset>
            </div>
            
            <div class="slds-form-element slds-m-top_medium">
                <label class="slds-form-element__label" for="feedback-textarea">Tell us more</label>
                <div class="slds-form-element__control">
                    <lightning-textarea
                        id="feedback-textarea"
                        placeholder="Give feedback..."
                        value={feedbackText}
                        onchange={handleFeedbackTextChange}
                        max-length="500">
                    </lightning-textarea>
                </div>
            </div>
        </div>
        <div class="slds-popover__footer">
            <lightning-button
                variant="neutral"
                label="Cancel"
                onclick={handleCancelFeedback}
                size="small">
            </lightning-button>
            <lightning-button
                variant="brand"
                label="Submit"
                onclick={handleSubmitFeedback}
                size="small">
            </lightning-button>
        </div>
    </div>
</template>
3. CSS Code (afAgentforceFollowUpActions.css)
.thumbs-container {
    display: flex;
    background-color: #f3f2f2;
    border: 1px solid #c9c7c5;
    border-radius: 0.25rem;
    overflow: hidden;
    margin-left: 1rem;
    position: relative;
}

.thumb-btn {
    background: none;
    border: none;
    padding: 0.5rem;
    display: flex;
    align-items: center;
    justify-content: center;
    min-width: 2rem;
    min-height: 2rem;
}

.thumb-btn:hover {
    background-color: #e5e5e5;
}

.thumb-btn .slds-button__icon {
    fill: #706e6b;
    width: 1rem;
    height: 1rem;
}

.thumb-btn:hover .slds-button__icon {
    fill: #444;
}

.thumb-up {
    /* No border between buttons */
}

.thumb-down {
    /* No border needed for the right button */
}

/* Feedback Popover Styles */
.feedback-popover {
    position: absolute;
    top: 100%;
    right: 0;
    z-index: 9001;
    width: 320px;
    max-width: 90vw;
    margin-top: 0.5rem;
    box-shadow: 0 2px 12px 0 rgba(0, 0, 0, 0.15);
}

.slds-checkbox {
    position: relative;
    display: block;
    margin-bottom: 0.5rem;
}

.slds-checkbox input[type="checkbox"] {
    position: absolute;
    opacity: 0;
    width: 1px;
    height: 1px;
    border: 0;
    clip: rect(0 0 0 0);
    margin: -1px;
    padding: 0;
    overflow: hidden;
}

.slds-checkbox__label {
    display: flex;
    align-items: flex-start;
    cursor: pointer;
    font-size: 0.875rem;
    line-height: 1.25;
}

.slds-checkbox__faux {
    width: 1rem;
    height: 1rem;
    display: inline-block;
    position: relative;
    flex-shrink: 0;
    border: 1px solid #c9c7c5;
    border-radius: 0.125rem;
    background: #fff;
    margin-right: 0.5rem;
    margin-top: 0.125rem;
}

.slds-checkbox input:checked + label .slds-checkbox__faux {
    background: #0176d3;
    border-color: #0176d3;
}

.slds-checkbox input:checked + label .slds-checkbox__faux::after {
    content: '';
    position: absolute;
    top: 0.125rem;
    left: 0.25rem;
    width: 0.25rem;
    height: 0.5rem;
    border: 2px solid #fff;
    border-top: 0;
    border-left: 0;
    transform: rotate(45deg);
}

.slds-form-element__legend {
    font-weight: 600;
    margin-bottom: 0.75rem;
}
