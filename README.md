

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
