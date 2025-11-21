        <!-- Jira 178, Feedback Popover -->

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
