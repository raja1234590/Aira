 UX Improvement: Enhanced Navigation in Rule Creation/Editing Flow

Problem Identified

When users navigate to create or edit rules (`/rules/new` or `/rules/[id]`), they lose access to the bottom dock navigation (which only appears on `/` and `/workspace`). This creates friction because:

1. **Lost Navigation Context**: Users only had a small back button in the header, making it unclear how to exit the flow
2. **No Clear Exit Path**: There was no prominent "Cancel" option, forcing users to rely on browser back button
3. **Inconsistent Navigation**: The back button behavior was unpredictable, potentially taking users to unexpected pages

Solution Implemented

Added prominent Cancel buttons and improved navigation logic to make it easier for users to exit the rule creation/editing flow.

 Key Changes

1. **Header Cancel Button**: Added a visible "Cancel" button in the header (next to the title) for quick exit
2. **Bottom Cancel Button**: Added a Cancel button in the bottom action bar alongside the Save/Create button
3. **Smart Navigation**: Cancel buttons intelligently navigate to the workspace page (where rules are managed) instead of using browser history
4. **Improved Back Button**: The back arrow now uses the same smart navigation logic for consistency

Files Modified

 `apps/aira-web/app/(app)/rules/new/page.tsx`
- Added `X` icon import from lucide-react
- Implemented `handleCancel` function with smart navigation
- Added Cancel button in header (replaces empty spacer div)
- Added Cancel button in bottom action bar (side-by-side with Create button)
- Updated back button to use smart navigation

 `apps/aira-web/app/(app)/rules/[id]/page.tsx`
- Added `X` icon import from lucide-react
- Implemented `handleCancel` function with smart navigation
- Added Cancel button in header (next to delete button)
- Added Cancel button in bottom action bar (side-by-side with Save button)
- Updated back button to use smart navigation

 UX Benefits

 **Multiple Exit Points**: Users can cancel from header, bottom bar, or use back arrow  
 **Clear Navigation**: Cancel always goes to workspace (predictable behavior)  
**Better Visual Hierarchy**: Cancel and Save/Create buttons are equally prominent at bottom  
**Consistent Experience**: Same navigation logic across create and edit flows  
**Reduced Friction**: Users can easily exit without losing their place in the app

 Technical Details

The `handleCancel` function checks the referrer to determine where the user came from, but defaults to navigating to the workspace page (`ROUTES.WORKSPACE`) since that's where users typically manage their rules. This provides a predictable and useful navigation target.

 Testing

To test the improvements:

1. Navigate to `/workspace` → Click "New Rule" → Verify Cancel buttons appear
2. Click Cancel (header or bottom) → Should navigate back to workspace
3. Navigate to a rule → Click Edit → Verify Cancel buttons appear
4. Click Cancel → Should navigate back to workspace
5. Test back arrow button → Should also navigate to workspace


